# Micro-CMS v1 - Hacker101 CTF Writeup

**Challenge Link:** [Micro-CMS v1 @ Hacker101](https://ctf.hacker101.com/ctf)  
**Difficulty:** Easy  
**Category:** Web  
**Platform:** Hacker101


## 1. Recon

Open the challenge in your browser and explore the available pages. There are a couple of pre-existing pages you can view and a button to create a new page. The website as no css, it looks really bad...

![Homepage](/img/writeups/MicroCMS/image.png)

Click into the **Markdown Test** page to see how content is rendered.

![Markdown page](/img/writeups/MicroCMS/image-1.png)

The editor indicates Markdown support and shows an edit button. Try editing to see how input is handled.

![Edit page](/img/writeups/MicroCMS/image-2.png)


## 2. Flag 1

It say that script are not supported,  but lets try it anyway, so we add a simple xss vulnerability on the title and the description and save it:

```html
<script>alert("XSS")</script>
```
It seem like the script is not executed but lets go in the home page, maybe its executed there.
And here we go, the script is executed, so we have a XSS vulnerability.
![alt text](/img/writeups/MicroCMS/image-3.png)

## 3. Flag 2

The `<script>` tag was blocked or not executed in the description, so try a different vector that often bypasses naive filters: an image tag with an `onerror` handler.

Insert into the description:

```html
<img src=x onerror="alert('XSS')">
```

Save it and, Here we go, xss vulnerability!
![alt text](/img/writeups/MicroCMS/image-8.png)
But no flag appear, let try to find it in another place like console or inspector. Inspecting the page with the browser inspector revealed the flag!

![alt text](/img/writeups/MicroCMS/image-7.png)


## 4. Flag 3
While creating pages, notice the URL pattern when viewing pages ends with an index:

```
/page/0
/page/1
/page/2
/page/3
```

Trying `/page/4` returned a **403 Forbidden** error.

![403 Forbidden](/img/writeups/MicroCMS/image-5.png)

However, direct editing URL access remained possible. Visiting the edit route for that ID:

```
/page/edit/4
```

allowed viewing the page content (because the edit route did not enforce the same access control). The third flag was present on that edit page.

![Flag on edit page](/img/writeups/MicroCMS/image-6.png)


## 5. Flag 4
When you edit a page, you can see that the URL is like this : `http://[some random character].ctf.hacker101.com/edit/1`, Let try a SQL injection

I try to add a `'` at the end of the URL like this : `http://[some random character].ctf.hacker101.com/edit/1'` 
And boom, the second flag is here!
![alt text](image-4.png)

## 6. Tips

* When you suspect XSS, test multiple vectors: `<script>`, inline event handlers (e.g., `onerror`), SVG, `javascript:` URLs, etc.
* Always inspect the DOM and network requests — flags or secrets are often placed in hidden elements or comments.
* Enumerate sequential resources (`/page/0`, `/page/1`, ...) and check both view and admin/edit endpoints for inconsistent access control.
* Try small URL tampering tests (add quotes, comments, or boolean logic) to see whether input flows into a query or error page.

## 7. Conclusion

GG! 🎉 You did it, Micro-CMS v1 completed!  

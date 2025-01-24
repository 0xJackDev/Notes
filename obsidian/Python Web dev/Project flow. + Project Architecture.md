

How does a typically website handle When someone Visits a website? what is the typical Flow Process.


Step 1: Find the IP address of the domain with DNS

Step 2: Assuming the IP address is found Your browser attempts to connect to the web server for the site you are trying to accesss

Step 3: After a reliable connection is established, we can send a HTTP request to the server. This is telling the server what we actually want to get from it. 


Step 4:  After the client sends the HTTP request to the server. The server now handles the request and delivers it back to the Client who initiated the request. This response includes multiple parts, 1. The version of HTTP being used, 2. A status code for the response indicating if the response was successful or not, or if redirected or not, and how the HTTP server handles it. Then it will also Return the Response body which includes the Content in which the Web server requested. (html data).

Step 5:
Assuming the server was able to fulfil the request to view the desired page, the browser is going to be server a document as part of the response.
This document describes the structure and meaning of the pages content,, and will contain links to other resources which also get fetched by the browser. This includes stylesheets, which describe the appearance of the pages content as well as images, videos and javascript files.

We will focus on the HTTP response and requests in these notes.






### [Flow content](https://developer.mozilla.org/en-US/docs/Web/HTML/Content_categories#flow_content)

Flow content is a broad category that encompasses most elements that can go inside the [`<body>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/body) element, including heading elements, sectioning elements, phrasing elements, embedding elements, interactive elements, and form-related elements. It also includes text nodes (but not those that only consist of white space characters).


https://developer.mozilla.org/en-US/docs/Web/HTML/Content_categories#flow_content




## Starting a new software project

These are the five stages in a waterfall process:

1. **Analysis**: where users are consulted so developers can find out what they want, and build a set of requirements. These requirements are what developers implement later on in the process.
2. **Planning**: each requirement is planned fully from design to the technical implementation. Often, you'll see documents explaining how certain features will be coded.
3. **Implementation**: everything is coded.
4. **Testing**: the finished app is tested (often by a separate team from the development team).
5. **Evaluation** or **Maintenance**: users use the product and bugs are fixed (forever).

Each step is long, and often the outcome of each stage is a lot of documentation or code.





First before we even make our website. Its good to start designing a Layout of the website in figma. Since you will need two designs for Mobile and for Desktop view. Make sure these are seperate. And make sure you do the Mobile first as it allows you to focus on what you need.




What is an SVG? SVG vs bitmap
Why we use SVG instead of a bitmap image

An SVG or a scalable vector graphics image is a type of image that instead of being defined in pixels is defined by mathematical functions.

That means that, in theory, we can expand or contract an SVG image endlessly without any loss in quality.

In contrast to this, traditional images that are defined by pixels are called **bitmaps**.

Here's an example of a bitmap image at three different sizes, compared to an SVG image:

![Example of scaling SVG and PNG](https://python-web.teclado.com/assets/img/scaling-images.7df55085.png)

You can see that as the bitmap image gets larger, the number of pixels doesn't _increase_. The pixels get larger, so they are more obvious.

## Embedding SVGs inside HTML documents

The language used to create SVGs is very similar to HTML because both derive from the same parent language: XML.

This is what the code for a simple triangle looks like:

```
<svg width="82" height="71" viewBox="0 0 82 71" fill="none" xmlns="http://www.w3.org/2000/svg">
    <path d="M41 0L81.7032 70.5H0.296806L41 0Z" fill="#C4C4C4"/>
</svg>
```

You can see that it is similar to HTML: there are tags and attributes.

We won't cover how to code your own SVGs[[1]](https://python-web.teclado.com/section06/lectures/09_what_are_svg/#fn1) in this course, since Figma will do that for us with a visual interface. However, it is something you _can_ learn. Understanding the code can sometimes be handy though, as you can do things like modify the size (using the `width` and `height` attributes of the `svg` tag).

Once we have that SVG code, we can just put it inside an HTML document. The browser will be able to understand it, and draw the SVG for us.

### [#](https://python-web.teclado.com/section06/lectures/09_what_are_svg/#drawing-an-svg-with-the-browser)Drawing an SVG with the browser

Let's create an HTML file, which I'll call `example-svg.html`. Inside it, just put the SVG code from above.

Then, open it up with your browser by right-clicking the file.

You'll see something like this:

![Example HTML page with SVG content](data:image/png;base64,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)

Try changing the SVG code, and see what happens! You'll see that by changing the `width` and `height` properties of the `svg` tag, the image changes in size (even without changing the `path` tag)!

The `viewBox` property controls how much of the SVG you can see, while `width` and `height` tell the browser how many pixels to draw on in the page. Later on we'll learn how to change the width and height using CSS.

## How to include an SVG in your HTML document

We've learned that we can embed the SVG code directly in our HTML documents. However, that can sometimes make the HTML code a bit messy (particularly with those longer SVG images!).

So instead what you can do is save the SVG code as a file, and place it in the same folder as your HTML document.

For example, you could have this folder structure:

```
my_project
  | - home.html
  | - logo.svg
```

Then, we can write some code in the HTML document that will take care of telling the browser to load the SVG and display it in the correct place.

We'll do this in our existing code, inside the `<header>` element:

```
<body>
    <header>
        <img src="./logo.svg" alt="The Microblog Logo" />
    </header>
    <!-- The rest of the code continues as per earlier lectures -->
</body>
```

When the browser loads this HTML document, it will run through it and find the `img` tag. Then, it will request the SVG from the server (or, in this case, our file system).

It will load the SVG image and then place it inside the `body` element.

![Working HTML document loading the SVG](data:image/png;base64,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)

If for any reason the image cannot be loaded (e.g. we misspelled it), we'll get a "broken image" symbol and the alternative text (the `alt` property) will be shown.

![Broken HTML document with misspelled SVG, showing broken SVG loading](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAUUAAACICAYAAABwdfmDAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAAGdYAABnWARjRyu0AABS5SURBVHhe7d0LcFRVngbwL4gojK4zklKeDl2jArskKuMoCaOzG6XAlfJBClcS0YWsVUa2akYLX4Vkq5KwvhhlqHFi1RrYxXRQGSKxZkpQiI5KglqDmDCzou40yiPAhPEBkoSk03v+597bfbr79iPdnSbB71d1ofu++nQn/eV/zrmd5LT/9WgAgRxogQBg3yQ61fS3Y471DZmTo75N1X2iTIv8PssJKPoeERFhmP0/EREpDEUiIgNDkYjIwDHF05Df70dPrx/+Pj/6+mSCgl9iomQxFE8jJ3t60X3yJEOQKA0MxdNAT68Kw+6T6PsufynluduXVRClg6E4xEkgdnZ12/e+o+Q7mHlIGcKJliGst9fPQBQMRMoghuIQ1dfXhxNdXfY9IsoUhuIQ9V0LxJdfetm+RTSwMj6m2NPTgz/u3KVvz7j6J/r/bNvx/gd6nOnH0y/HmWeeaa8dWCdOnMDrW9/Ezg934Yt9+/W6iyZOwJTJl+KWm27EqFGj9Lr/WvM/uHvxXfp2qmSWuau7f91mad87b7+NtrbdOHDggF43fvx45OVNwzXXXhts32AloXjbv9xm3yMaOBkNRScQjx0/jnPPPQczrjp1oXjsmGrDOedkJRjf2d6C9S9uwInOTntNuFEjR2LB7fPx8Z5PsL15B/77+Rp7S2qOffttv345wvvvvY9NmzahU7Vv2rRpOgyFhOPu3bsxUrXvlltuwVVXX6XXD0YMRcqWjIViZCD++IrsVWmRdFtUxZaNYJRArF27Tt+eWTgDs68vwkUXTdT3v/hiH7ZsbdJBaEonFPs72yyBuH79eowfNw6LysowevT59hbL0aN/w9raWhw4eBCLyxapyjHf3pJYW+19WNNm37FNK3sGZRdsxWOPfYCfPPIIrr8QOLz1MTz++Vw8U5Zn79V/qYRi6xOXY6HXviNK1+Gjh+I9vw40llcAVb/BzO334rqP74nev/UpXFYzGdtqbkKuvSo7Qm3z1KrnhUTPJYPkOb82Gx+V7UV5UQWa7dWO0rpdeDBLTcmGjIwpDqZAFPLY0gZpi7RJ2iZtzDTpkkqFKMoW3am7xU4gCrkt6yZfeom9Jn0y45wsaZ9UiBKISx98IBiI9/3iPr0IWSfbZJ/19S/qY/rjgrkP45lVzwQXnXsXXo9HVlmBeGq04sl8OzhadwWXF7BFbYmjdS0qMAczs5t2yTHalv+Qej7ZCkQJ4xovSm9wHq8ULxiv6UdNlfDdcTkueyLuKzukpB2Kgy0QHdkIxi1vNOkus1SI18wssNeGkzHEPZ98at9LX1+gz76V2Nt/eFt3maVCTET2kX3lmKFNKqo74avaGhUc+Q89gHhR0vqaevOXZ7sCTM4pa1tHMzajEotjvXC5N6GmdR1Kvc+hscNeN8SlFYqDNRAdAx2MMqkipMvsRgIxsuucLvksc7J2t7XpMcTILrNT1ZlkH9lXxhjT14baXzyGrYftu5HaaoPV6n3x9kuFvIm3l6L85jjxId3B/KciqsZWbPaWYk4/CzDpol+mqlK9lL+qItlhVavOtvJgYkhoX44nG19FuXFMR+O9ofMkaJveN6wyC3+syONjnztWG0M6tm8G5hQmCON8zCmV1904Xr/GoXNHV5LW6xDcrl8Hac+94eEq5wm+rvZr12q0W5/XPFfE8ZGPY7bDPner+fqo7WmFoh63U2EjZPzurbffxRvb3oy77HjvA71/JsiEittjmIu0SdomnGDMlH37rVlcs8tskq6zjB9GLunozxCwjBM6kyoms/tskn2dmekBI4FYCyx2utxlF+D3tVuRsVw8uAfNMydjnH03WR2Nz8FbOjtuJRlFvakW7q3ENrsrua18krNBvWnvBOqcbuY6eJZXhL1ZvSprqmSbjE12vIrlyz2hbmndbHsvS/y2WY+lK2P7+G1VPix0giTmuRO3UfZZs1xlYhLjCeOmFKL544PWHQmbO3yobHLOvRWVe++M+MFwPTbPCbX5hTn2piR479iCOXabS713qjCTsVb7PCqcK2qd4It8HKsdT5r5vL0CNaoS1tubKlGozpf96xRP9acP+OmHjDryu8eNqq9W1Yjxtb2/GxfMnYvglEveXNyID9CWyWoxkfwH1JvA7Ep3QAqiyrJ+loli+x7YUYDc/HyromrdAu9Ms8uZj8VVCKukorvCPviczeo8SbfNfqwqozLOvfkelKqDQg/ncu4k2qj3Kb0H8YpuN9LVL6yqNI7Lxc3lpWje3GwFtR4fDW9z/s3JDw2U1jlfO6lQZUWojfk3qBV791qPE9VrsNrhfc1IRfO1y70JanN6oeh0TYXM8v7jtT/FrOv+Ke6Syct05Fxuj2Eu0iZpm3C6+JkycYJVhckscyIygbH62efwSuPv7DWpcf6WRDJk8qQ/lZ/sK8f0R/hES1ko7FwdxmEVfuFB+jh+f+QIPj9i75KucZNRaARVUvS4WT8mWCZNst7AEq51wMKIbluHz6crkOucLplarlveHKqkIsm4XNMcbC6y9g2rZBK0TT+W056gcZg8sxl75OFinDuZNupxzOAES3wHP25G4RT53umAby/g8UQ02Pi6uLc5NVKhWo/rQnoN8NpfH3u5wxsKzRjSCsVszfKmaqDHPKfbASuX3STifXEDdn74ETqOHrXXpGZYP0JxWl6eHiOUy24SkX1kXzlm4FyICy+0LtsJBam1pHG1TrjcQtXd82KzGSwJtNaq7lfEuFmux+P65tFvaJOuOqXrJcFjBaM+Vi7/0V02Y4k3Y6wnLGS/dcAdofBya5spVjuBQkx2ssLl3AnbqLrdNcmOsdr7WhVZLjyTVG0aLE0N9rBG7DZnmASxqgSd4Y3gkuByqrS7z4M1GLMxCTR7VhFGjjxbT6bI9YqxyDZnwuXWm+bq/1N1xhnJf8mu/dm1+sLstWvW2Gtik2sVZV85ZiDlXTUNu9VjJepmp87uIqk3f+TEQesT9iSDngRwJhysSYyoiZn82aoLWoHl5jn0+FyoK9vR+FRoDC53EtRb3SLHeiPGruJR7QntK1WefTNW20wu7exorAhdWhTr3AnaqCdYqhYZ3fgY5LUsqoAn2KVVp1Zd2Oaw8ckONKr7wXB3aXNro4yBWhVuqAvfiielskuV/IBUr0TY1zAJGRlTHGzBmI1AFPLRuJLbrQuK5QLu59esC+tKyydYZJ1zcbdcy5ibO1rfTtXw4cPtW4lJ++STKtItXvnUymDF6FRnQtbJNpmUWVBy+8B/3C+vDA/PPYI1we6zWv4zgxMtQldvMnFwfajbpJaaKS5vcj1u5jaJkY8HI89RpDqyTb8Jjl/lqhSssLull+lJC2ebOta5fs85NmpW1KAqmtC+1sSAvhg6ZttM0e28bvOc0MXlsc4dt43WOKb7BEtEd1QuZFfVV9jF23pYwWO8Ntbj1gTDPbrNCz+W7rT6gVZVCQTXb8GcOhk0TJU6X03090GiH1Y5Gf+Yn/FJklP52WfdhgEMRJNcmiOX33R2uv+SBqkmJTxjXcvYX8dPdOrfkpMs82N+eap7PH681a86cOAg2tradIUogdifT7Nk28B8zM+andxTPhg/kRG7bXIZUM0UM2QyTKq/U/KpncEho6EonGAUp/KzzyIbgeiQiRS5mFsCUi7VkSC8aOJE/QshpJudyQpMPtXS39+SI+2TC7Pl2kWpCoVMqsgYonSZv5O/EEJ1h8tVd7hqML75Y7ZNLqV5DpONijXTJHQ333B6fXSvPzIeipQd/a0Whzr+QgjrukIZYSusGsAqkRiKQ5UEogQjEWVWRiZaKPuGDRuGkWefZd8jokxhKA5hZw4fjlFnn23f+w5jX4cyiN3n04D+ey2dXfwTp/wTp5QBDMXTCP8YPlH6GIqnIb/fj55eP/x9fv2rxvglJkoeQ5GIyMCJFiIiA0ORiMjAUCQiMuR88tlejikSEdk40UJEZGD3mYjIwFAkIjIwFImIDAxFIiIDQ5GIyMBQJCIyMBSJiAwJr1Osq6uzbyWWn5+PKVOmYMSIEfYaIqKhJWEovvBCHYpm/TP+7rwfxPwFxzlqyx+atuDI4XZMnfr3mD79Cpx1Fn9VPhENPQm7z5KZx7oC+Os3fTj8ld91OXrMj5O9AVx55ZX4/vfPw7vvvouufv4JTiKiwSCJUOxTgQd8292H4119GDkiB5eMHY4Jo8/Q92XpVNucv7Y5depUXHLJJdiyZYv+W8PYsQI5OTlxlxU75MgWrFC3i9cf0udJ3SHU3xY6d9zz7a9Hsb1fTs4K1QJnXTHq9+s9BoDdvir9aO70a2a3J9Ncvh7W609EImEoOr+5WTrZ488/Q4ehkHDM/+EIDMtR29T9Xn8v3nrrLaxevRqbNm3Cvn378dJLL+OQbyfm1bfb52iHdz6M+wE0V8rZJBAL8ajcTNsYlLyszt1Sre81vNKkYshdy9pSNMiNymbVlmUokNsTSrAxsBElE+ROpkkgjkXpBvuuGwmtgsy8Eq5mLAt+HaznHcCyGdYmIkqy+yyh96Mxw3HBeVYghgR0aHZ19+Lqn87GgruWYOHiJbir7N9xS/Ht+ligGEsXjLF2d1GwyAuPiqNlgWZYMZY51ZXqjBtKUetWCamKcGVbNaolpC/22CsHmgS2HUixSGjZgT7Qsve8iYaOJCpF1S9W2fbpwW68/+mJsOWP/9eJHr/qOucMwzddARz5ugftX/bg8Ne9+KZTArMPYxaUWBVYLKoyKxmoSmVWmQ6gR5+uj6oWD72zEbi1SAUyEVFIUpWi/OlMv6oIYy09vX040e1XQejH1yf8OKb+7+qxusepOLS+2B7vihzbs8Ydkx8LU5XZ/W7VYgtqS6arCtYlEt3G88LG4cw2OeOg9Xa7nG3h45qxxgdbqkL7JHwuEWOBkWOlodfMXNIfG408b2Q7zecQWkLPN9HxRINNUpWi7kKrfAuoAExqUfueP3o07r773+yzJK+hZCyW4Fl1DulmNqB0rfP2kgBqQpFui1r2ebGzIIk3/QyXanFHE3bWl0VXsG7jeXod0Kwf127T/XKu0DhoQ4nPbpeMRVrjhhtvNcdRH0VhZDBWFKJplvVcZFz10XjPJawNalHda3mdgsGoto8tAbz7QucDqtX+6Y2NSqCNfaUY7fbjttfPU+0MBZtsL6yQx5Ht9rDAfK/a3xqfTXQ80WCUdPc5oP6Tm9YSwEl/Nzq6PseX3QdVF7rH2AZ876wcTMpNeGpXMgmzUY9BjoEnz1onDq1fqQJIwsWuOibKJEkDNr4TaxrFMcauFjeiyanint6J4mtcxjmjxvNk30dR3WJPwjiTOC+XqFuhcdB5ZsDuqEXphmpjHFUd87QXKg7QZIZBZXNwgqNguZwn1nOx2hD2GKqdEnzOJJJMZmF+MYrsACyYJa3aCV9aVaJU0w2ovl+eq2XMgmetHzBvWPHu+6xBPY+i4GtTdOs89Tr74NP3Ex9PNBgl1X2WTrBfpZ38PeEvu/Zj++Fa1PzvXKzfezfqfP+Kl3z3Ys9Xb6Kz5xuMPX84pk482zo40+zZUnOxAjSBGUU6dHTVKaGVtzTJCkq9wePNFLvQARVpggfT1X87fbEC3AOPVFmu3NvguTgUQGMWLEW1MUQQGZIp2e9TsRrJ/kHV5tNhLJNk8ypWBivcsJBM4niiwSipSlHGFFVxiAOdbWg++jx2fb0Bw4bn2HsAX/Z+jjeP/BJ957TgR2OtQOzo6MCvf/2svp0xKb+ZClCmum5Qb+BiqfxmBWuuBKywih1m0cZ4JP4iqkLbdE+sALeCz3271QbXS4vmq236hvX8pGsqVfTYkulo1tVsCvbXY4V0y+0gd63q8jzWuSeUYGml+mEz0XrcwjbVdV5uv7bJHE80CCVVKYojXX/GR1/9Fnu/lW9ya53p51dXYvbFxfr2sc4A/nLEHzw2UsNnVgerP5xqaKx50bN6A9fHGZ8yw0wfrzvcXpRFzHZHt8fpelpdwoaSJWHjfS1VcS6sdsYwC8zJBtX1nx/xuEbAt1QVRm832uBMFi0JTq5EdE1lTPGzpUYF7XT344t+3i1YMXEjPHpowflBUhgaA5TLmCrmwbvIOruMGa68OHTNqTWs4Eh8PNGgpL6Z41q1anVg24d/DvxH08OB0ld+Fri9oSBq8X31ib13IPDmX14PPP3O6kBL20F9bFBLtSSksVQHmu1NAXVLve2D2+bVtweaK41953sD7bLbPm9Avc2i14dpD6hQct2nvX5eoLrFvuPWnrB18wLefdaucpy5r7TPrc0hsdtgidheGXolwtsVakNke4PPQ0S+Ls5intcR9bwjloi2hj93oz0ixrnM1yLu8USDUI78o75hY1q16lf4+tJD2N/XhuM9f7PXWkadeQ5Wz27A99T/Yl3br/DaZy/hB2eNw8UjVDXwp2G4/+f36W00gFSluALLoj+ZskNV0nId6IB8OkcqxRVoumZZ1PkPra+HL9H1qUSDVMLuc2dnJ4Z/eC5+uKsA//CnG4NLUcdi1M59PRiIGzb8Fl80Htfbxu28Ap3vdcPf49fbaCCpLq/rxwLV+jc8AxaI0hVeUuIyqaTW18KZkSYaehJWijQE6OsYI4NRrh9MbmwxVfo6xBL96fEQuU4x1UkeokGAoUhEZEjtCmsiotMUQ5GIyMBQJCIyMBSJiAwMRSIiA0ORiMjAUCQiMjAUiYgMDEUiIgNDkYjIwFAkIjIwFImIDAxFIiIDQ5GIyMBQJCIyMBSJiAwMRSIiA0ORiMjAUCQiMjAUiYgMDEUiIgNDkYjIwFAkIjIwFImIDAxFIiIDQ5GIyMBQJCIyMBSJiAwMRSIiA0ORiMjAUCQiMjAUiYgMDEUiIgNDkYjIwFAkIjIwFImIDAxFIiIDQ5GIyMBQJCIyMBSJiAwMRSIiA0ORiMjAUCQiMjAUiYgMDEUiIgNDkYjIwFAkIjIwFImIDAxFIiIDQ5GIyMBQJCIyMBSJiAwMRSIiA0ORiMjAUCQiMjAUiYgMDEUiIgNDkYjIwFAkIjIwFImIDAxFIiIDQ5GIyMBQJCIyMBSJiAwMRSIiA0ORiMjAUCQiMjAUiYgMDEUiIgNDkYjIwFAkIjIwFImIgoD/B2IT1dzqrgnWAAAAAElFTkSuQmCC)

Other image types

You can include any image type, not just SVG, with the `img` tag. For example:

```
<img
    src="./my-image.png"
    alt="An image showing something very interesting"
/>
```




HTML FORMS:

THe form element has three main parts.
- The `<form>` element itself, which describes how the form behaves in terms of sending data.
- A button used to submit the form, and send data as described in the `<form>` element.
- Form inputs, each of which is comprised of a label and a field.


There are two ways of submitting data in forms. Using a GET request (the default) or using a POST request. This is the method

In addition to the method, we can specify an **action**, which is the URL that will receive the form data.

This form uses `GET`, and the form data is sent to `/entry`:

```
<form action="/entry"></form>
```

If we don't specify an `action` attribute, then data is sent to the _current URL_:

```
<form></form>
```

We can manually specify the method (with or without an action):

```
<form method="GET" action="/entry"></form>
```

And we can use `POST` instead of `GET`:

```
<form method="POST" action="/entry"></form>
```

## Sending data with a form

But what are the differences between `GET` and `POST`? To understand this, let's add a text field and a submit button to our form:

```
<form>
    <label for="sample-field">Sample:</label>
    <input type="text" name="sample" id="sample-field" />
    <button type="submit">Submit</button>
</form>
```

If we open an HTML file containing this with our browser, we'll see something like this:

IMAGE

Let's type something in our field, and press Submit:

IMAGE

Now notice that the page seemingly refreshes. The form is emptied. That's because the form sent the data to the URL defined in the `action` attribute. But since we didn't add an `action` attribute, the default is the _current URL_.

However, notice that the URL changed slightly. We ended up with `?sample=Bob` at the end (if you typed "Bob" in the field).

That is the form data that the form sent to the current URL.

So the form sent the data to the current URL, which means that it made another request to our HTML file. Our HTML file doesn't _use_ the form data for anything (we'll learn how to do that later), so all that happened is the browser loaded the HTML contents and painted them again


### GET requests and query string parameters

Whenever we send form data using `GET`, the data will be appended to the URL as query string parameters.

Query string parameters are key-value pairs appended at the end of a URL. They are a standard way of sending non-sensitive data in web requests.

If you have more than one, they'll be separated by ampersands:

```
?sample=Bob&last_name=Smith
```

### [#](https://python-web.teclado.com/section06/lectures/12_html_form_send_data/#post-requests)POST requests

If we change the form's `method` to `"POST"`, reload the page, and submit again, you'll see no query string parameters.

When we send data with `POST`, data is included in the **body**, a different part of the request, instead of being part of the URL.

Data in the body is a bit more secure because it's not visible in the URL. For sensitive information, we should use `POST`.

Also, there are limits to the size of URLs which means that for very long forms, `GET` might not be viable.
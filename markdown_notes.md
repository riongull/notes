# Markdown Notes

## Rendering markdown
* atom: ctrl-M
* visual studio code: cmd-V

## Links to good references
* [official markdown specification](http://daringfireball.net/projects/markdown/syntax)
* [basics from github](https://guides.github.com/features/mastering-markdown/)
* [more advanced from github](https://help.github.com/articles/working-with-advanced-formatting/)
* [more advanced rules on lists and whatnot from some random dude](https://gist.github.com/dupuy/1855764)

## Creating fenced code indents ([source](https://gist.github.com/clintel/1155906))


#### fenced code blocks inside ordered and unordered lists

1. This is a numbered list.
2. I'm going to include a fenced code block as part of this bullet:

    ```
    Code
    More Code
    ```

3. We can put fenced code blocks inside nested bullets, too.
   1. Like this:

        ```c
        printf("Hello, World!");
        ```

   2. The key is to indent your fenced block by **(4 * bullet_indent_level)** spaces.
   3. Also need to put a separating newline above and below the fenced block.

---

#### failed attempts:

1. This is a bullet.
2. This is the end of the first bullet list, with a fenced code block following:

```
Code
More Code
```

3. This is the start of a new bullet list. Hey, where is my fenced code? ```
Code
More Code
```

4. Maybe we can do it with indenting?
    Code
    More Code
5. Did that work? No, so we will try with separation:

    Code
    More Code

6. Now I will try more indenting, to match the bullet margin, plus 4:

       Code
       More Code

7.  Well that was disappointing. How about we indent and use backticks together?
       ```
       Code
       More Code
       ```
8. No such luck.

---

* Oh look, it's some [Apache config](http://pygments.org/docs/lexers/#lexers-for-non-source-code-file-types):

    ```apache
    <Directory /foo/bar>
      Order allow,deny
      Deny from all
    </Directory>
    ```

* Wasn't that fun?

---
layout: default
title: Use Mako template engine in webpy
---

# Use Mako template engine in webpy

### Problem
How to use Mako template engine in webpy?

### Solution

You need to install both Mako and webpy(0.3) first: http://www.makotemplates.org/. And then try out the following code snippet:

    # encoding: utf-8
    # File: code.py

    import web

    from web.contrib.template import render_mako

    urls = (
            '/(.*)', 'hello'
            )

    app = web.application(urls, globals(), autoreload=True)

    # input_encoding and output_encoding is important for unicode
    # template file.
    # Reference:
    # http://www.makotemplates.org/docs/documentation.html#unicode
    render = render_mako(
            directories=['templates'],
            input_encoding='utf-8',
            output_encoding='utf-8',
            )

    class hello:
        def GET(self, name):
            return render.hello(name=name)
            # Another way:
            #return render.hello(**locals())

    if __name__ == "__main__":
        app.run()

Template file:

    ## File: templates/hello.html

    您好：${name}
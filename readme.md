Greenlet-Tornado
================

An easy way to seamlessly use Greenlet with Tornado.
----------------------------------------------------

This allows you to write code as if it were synchronous, and not worry about callbacks at all.
You also don't have to use any special patterns, such as writing everything as a generator.

Derived from this blog article:
<http://blog.joshhaas.com/2011/06/marrying-boto-to-tornado-greenlets-bring-them-together/>

Example Usage:
--------------

    import tornado.web
    from greenlet_tornado import greenlet_asynchronous, greenlet_fetch

    class ExampleHandler(tornado.web.RequestHandler):
        @greenlet_asynchronous
        def get(self):
            # ...
            self.helper()
            # ...
            self.write("Hello World!")

        def helper(self):
            # Fetch something. greenlet_fetch() will block until the request is complete,
            # but the tornado IOLoop can do other things in the meantime.
            http_response = greenlet_fetch("http://www.mopub.com")

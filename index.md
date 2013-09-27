---
layout: home
description: "SceneJs home."
tags: [Jekyll, theme, responsive, blog, template]
image:
  feature: grid.jpg
  credit: SceneJS
  creditlink: http://scenejs.org
---


# Quick Start

First, include the [SceneJS library](api/latest/scenejs.js) in the &lt;head&gt; tag of your web page:

{% highlight html %}
<script src="http://scenejs.org/api/latest/scenejs.js"></script>
{% endhighlight %}

Then build a scene. We'll make a spinning blue teapot:

{% highlight javascript %}
var scene = SceneJS.createScene({
    nodes:[
        {
            type:"material",
            color: { r: 0.3, g: 0.3, b: 1.0 },

            nodes:[
                {
                    type: "rotate",
                    id: "myRotate",
                    y: 1.0,
                    angle: 0,

                    nodes: [
                        {
                            type:"prims/teapot"
                        }
                    ]
                }
            ]
        }
    ]
});
{% endhighlight %}

And voilà, one blue teapot:
            <a href="examples.html?page=firstExample"
               target="other"> <img
                    style="display: block; margin-left: auto; margin-right: auto;" src="images/firstExample.png"/></a>
            <br>

Now let's start the teapot spinning:

{% highlight javascript %}
scene.getNode("myRotate", function(myRotate) {

    var angle = 0;

    scene.on("tick",
        function() {
            myRotate.setAngle(angle += 0.5);
        });
});
{% endhighlight %}

[Run this example](examples.html?page=firstExample).

To keep the core library small, SceneJS dynamically loads it's non-core functionality from a directory of
plugins. In the example above, the <code>prims/teapot</code> node is a custom node type instantiated
from a <a href="https://github.com/xeolabs/scenejs/tree/V3.1/api/latest/plugins/node/prims/teapot.js">prims/teapot</a>
plugin, which SceneJS loaded on-demand from <a href="https://github.com/xeolabs/scenejs/tree/V3.1/api/latest/plugins">the
plugins directory</a> within its repository on GitHub.

If you'd rather serve the plugins yourself, then just copy that directory to your server and configure SceneJS to load
them from there, like this:

{% highlight javascript %}
SceneJS.setConfigs({
    pluginPath: "./foo/myPluginsDir"
});
{% endhighlight %}

Want to write your own plugins? Excellent, please read more about the plugin API <a
 href="https://github.com/xeolabs/scenejs#plugin-api">here</a>.
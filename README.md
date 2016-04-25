<img src="https://raw.githubusercontent.com/lgrkvst/d3-sunburst-menu/master/img/observatory.jpg" width="400">

# D3 Sunburst Menu
A d3js multilevel circular (pie) menu, quite undocumented at the moment. Here's a [demo](https://rawgit.com/lgrkvst/d3-sunburst-menu/master/demo/d3-sunburst-demo.html)

Pie menus are _a graphical user interface for mouse gestures_. This particular implementation is traversed through nudging the edge and holding still (upon which the menu will traverse after a threshold of 0.3s).

## Description

* Visualise any tree structure as a traversable, circular partition menu
* Traverse and select nodes by nudging the edge
* Each leaf node should have a `function callback() {}`, invoked upon selection.
* Automatic gradients and curved labels, although if a level contains more than 10 children, it's recommended to add `["text-align"] = "radiate"` to those children, causing the labels to emancipate from the center.

sunburst_menu returns an object with a redraw function, so that the partition can be altered (in my case waiting for several REST services to return menu data) and then updated through a call to redraw().

##Installation
`$ npm install d3-sunburst-menu`

##Inclusion
Using webpack, in your entry.js file:
`var d3_sunburst_menu = require('d3-sunburst-menu');`

Initialize by:
`var menucontroller = d3_sunburst_menu(tree, node, svg_container);`

Don't like front tooling like webpack?
```
<script> var module = {}; </script>
<script src="local/path/to/d3-sunburst-menu.js" type="text/javascript" charset="utf-8"></script>
<script>var menucontroller = module.exports(tree, node, svg_container);</script>
```


###Arguments:

* _tree_ is a d3 partition tree with a BIG NOTE: "children" arrays must be named "_children" (with a preceding underscore). This in order to allow for a menu instance to be redrawn with new nodes. (Fixable, although not my top priority.)
* _node_ is any object with x and y properties (for instance a d3 force directed node instance). d3-sunburst-menu only uses the x and y attributes to position the menu inside the...
* _svg_container_ is the d3 selection that will host the menu (as obtained by `d3.select`).

Redraw by:
`treecontroller.redraw();`

Remove by:
`treecontroller.remove();`

##Settings
The first few lines of d3-sunburst-menu.js offers a number of settings:

    var _radius = 140; // size of menu
    var _rotate = Math.PI / 2; // default menu rotation (if you need to align menu items)
    var backSize = 0.1; // back button size as percent of full circle
    var idleTime = 300; // time (ms) between edge nudge and menu traversal
    var dropshadow = false; // add a nice dropshadow – sort of kills menu performance, but can be optimized



    @author Christian Lagerkvist [@lgrkvst, git@o-o.se]
    todo:
     Documentation
     Add icon support
     Fix leaf text styles (curved text demands some restrictions... There is a radiating text style in the source code, although somewhat neglected lately)
     Move svg attributes to css
     Add tests
     Refactoring?


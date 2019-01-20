# CodeHilite

[CodeHilite][1] is an extension that adds syntax highlighting to code blocks
and is included in the standard Markdown library. The highlighting process is
executed during compilation of the Markdown file.

!!! failure "Syntax highlighting not working?"

    Please ensure that [Pygments][2] is installed. See the next section for
    further directions on how to set up Pygments or use the official
    [Docker image][3] with all dependencies pre-installed.

  [1]: https://python-markdown.github.io/extensions/code_hilite/
  [2]: http://pygments.org
  [3]: https://hub.docker.com/r/squidfunk/mkdocs-material/

## Installation

CodeHilite parses code blocks and wraps them in `pre` tags. If [Pygments][2]
is installed, which is a generic syntax highlighter with support for over
[300 languages][4], CodeHilite will also highlight the code block. Pygments can
be installed with the following command:

``` sh
pip install pygments
```

To enable CodeHilite, add the following lines to your `mkdocs.yml`:

``` yaml
markdown_extensions:
  - codehilite
```

  [4]: http://pygments.org/languages

## Usage

### Specifying the language

The CodeHilite extension uses the same syntax as regular Markdown code blocks,
but needs to know the language of the code block. This can be done in three
different ways.

#### via Markdown syntax <small>recommended</small>

In Markdown, code blocks can be opened and closed by writing three backticks on
separate lines. To add code highlighting to those blocks, the easiest way is
to specify the language directly after the opening block.

Example:

```` markdown
``` python
import tensorflow as tf
```
````

Result:

``` python
import tensorflow as tf
```

#### via Shebang

Alternatively, if the first line of a code block contains a shebang, the
language is derived from the path referenced in the shebang. This will only
work for code blocks that are indented using four spaces, not for those
encapsulated in three backticks.

Example:

```` markdown
    #!/usr/bin/python
    import tensorflow as tf
````

Result:

``` python
#!/usr/bin/python
import tensorflow as tf
```

#### via three colons

If the first line starts with three colons followed by a language identifier,
the first line is stripped. This will only work for code blocks that are
indented using four spaces, not for those encapsulated in three backticks.

Example:

``` markdown
    :::python
    import tensorflow as tf
```

Result:

    :::python
    import tensorflow as tf

### Adding line numbers

Line numbers can be added by enabling the `linenums` flag in your `mkdocs.yml`:

``` yaml
markdown_extensions:
  - codehilite:
      linenums: true
```

Example:

```` markdown
``` python
""" Bubble sort """
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```
````

Result:

    #!python
    """ Bubble sort """
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]

### Grouping code blocks

The [SuperFences][5] extension which is part of the [PyMdown Extensions][6]
package adds support for grouping code blocks with tabs. This is especially
useful for documenting projects with multiple language bindings.

Example:

````
``` bash tab="Bash"
#!/bin/bash

echo "Hello world!"
```

``` c tab="C"
#include <stdio.h>

int main(void) {
  printf("Hello world!\n");
}
```

``` c++ tab="C++"
#include <iostream>

int main() {
  std::cout << "Hello world!" << std::endl;
  return 0;
}
```

``` c# tab="C#"
using System;

class Program {
  static void Main(string[] args) {
    Console.WriteLine("Hello world!");
  }
}
```
````

Result:

``` bash tab="Bash"
#!/bin/bash

echo "Hello world!"
```

``` c tab="C"
#include <stdio.h>

int main(void) {
  printf("Hello world!\n");
}
```

``` c++ tab="C++"
#include <iostream>

int main() {
  std::cout << "Hello world!" << std::endl;
  return 0;
}
```

``` c# tab="C#"
using System;

class Program {
  static void Main(string[] args) {
    Console.WriteLine("Hello world!");
  }
}
```

  [5]: https://facelessuser.github.io/pymdown-extensions/extensions/superfences/
  [6]: https://facelessuser.github.io/pymdown-extensions

### Highlighting specific lines

Specific lines can be highlighted by passing the line numbers to the `hl_lines`
argument placed right after the language identifier. Line counts start at 1.

Example:

```` markdown
``` python hl_lines="3 4"
""" Bubble sort """
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```
````

Result:

    #!python hl_lines="3 4"
    """ Bubble sort """
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]

## Supported languages <small>excerpt</small>

CodeHilite uses [Pygments][2], a generic syntax highlighter with support for
over [300 languages][3], so the following list of examples is just an excerpt.



### Diff

``` diff
Index: grunt.js
===================================================================
--- grunt.js	(revision 31200)
+++ grunt.js	(working copy)
@@ -12,6 +12,7 @@

 module.exports = function (grunt) {

+  console.log('hello world');
   // Project configuration.
   grunt.initConfig({
     lint: {
@@ -19,10 +20,6 @@
         'packages/services.web/{!(test)/**/,}*.js',
         'packages/error/**/*.js'
       ],
-      scripts: [
-        'grunt.js',
-        'db/**/*.js'
-      ],
       browser: [
         'packages/web/server.js',
         'packages/web/server/**/*.js',
```




### HTML

``` html
<!doctype html>
<html class="no-js" lang="">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="x-ua-compatible" content="ie=edge">
    <title>HTML5 Boilerplate</title>
    <meta name="description" content="">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <link rel="apple-touch-icon" href="apple-touch-icon.png">
    <link rel="stylesheet" href="css/normalize.css">
    <link rel="stylesheet" href="css/main.css">
    <script src="js/vendor/modernizr-2.8.3.min.js"></script>
  </head>
  <body>
    <p>Hello world! This is HTML5 Boilerplate.</p>
  </body>
</html>
```

### Java

``` java
import java.util.LinkedList;
import java.lang.reflect.Array;

public class UnsortedHashSet<E> {

  private static final double LOAD_FACTOR_LIMIT = 0.7;

  private int size;
  private LinkedList<E>[] con;

  public UnsortedHashSet() {
    con  = (LinkedList<E>[])(new LinkedList[10]);
  }

  public boolean add(E obj) {
    int oldSize = size;
    int index = Math.abs(obj.hashCode()) % con.length;
    if (con[index] == null)
      con[index] = new LinkedList<E>();
    if (!con[index].contains(obj)) {
      con[index].add(obj);
      size++;
    }
    if (1.0 * size / con.length > LOAD_FACTOR_LIMIT)
      resize();
    return oldSize != size;
  }

  private void resize() {
    UnsortedHashSet<E> temp = new UnsortedHashSet<E>();
    temp.con = (LinkedList<E>[])(new LinkedList[con.length * 2 + 1]);
    for (int i = 0; i < con.length; i++) {
      if (con[i] != null)
        for (E e : con[i])
          temp.add(e);
    }
    con = temp.con;
  }

  public int size() {
    return size;
  }
}
```

### JavaScript

``` javascript
var Math = require('lib/math');

var _extends = function (target) {
  for (var i = 1; i < arguments.length; i++) {
    var source = arguments[i];
    for (var key in source) {
      target[key] = source[key];
    }
  }

  return target;
};

var e = exports.e = 2.71828182846;
exports['default'] = function (x) {
  return Math.exp(x);
};

module.exports = _extends(exports['default'], exports);
```

### JSON

``` json
{
  "name": "mkdocs-material",
  "version": "0.2.4",
  "description": "A Material Design theme for MkDocs",
  "homepage": "http://squidfunk.github.io/mkdocs-material/",
  "authors": [
    "squidfunk <martin.donath@squidfunk.com>"
  ],
  "license": "MIT",
  "main": "Gulpfile.js",
  "scripts": {
    "start": "./node_modules/.bin/gulp watch --mkdocs",
    "build": "./node_modules/.bin/gulp build --production"
  }
  ...
}
```


### MySQL

``` mysql
SELECT
  Employees.EmployeeID,
  Employees.Name,
  Employees.Salary,
  Manager.Name AS Manager
FROM
  Employees
LEFT JOIN
  Employees AS Manager
ON
  Employees.ManagerID = Manager.EmployeeID
WHERE
  Employees.EmployeeID = '087652';
```

### PHP

``` php
<?php

// src/AppBundle/Controller/LuckyController.php
namespace AppBundle\Controller;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Component\HttpFoundation\Response;

class LuckyController {

  /**
   * @Route("/lucky/number")
   */
  public function numberAction() {
    $number = mt_rand(0, 100);

    return new Response(
      '<html><body>Lucky number: '.$number.'</body></html>'
    );
  }
}
```

### Protocol Buffers

``` proto
syntax = "proto2";

package caffe;

// Specifies the shape (dimensions) of a Blob.
message BlobShape {
  repeated int64 dim = 1 [packed = true];
}

message BlobProto {
  optional BlobShape shape = 7;
  repeated float data = 5 [packed = true];
  repeated float diff = 6 [packed = true];

  // 4D dimensions -- deprecated.  Use "shape" instead.
  optional int32 num = 1 [default = 0];
  optional int32 channels = 2 [default = 0];
  optional int32 height = 3 [default = 0];
  optional int32 width = 4 [default = 0];
}
```

### Python

``` python

"""
  A very simple MNIST classifier.
  See extensive documentation at
  http://tensorflow.org/tutorials/mnist/beginners/index.md
"""
from __future__ import absolute_import
from __future__ import division
from __future__ import print_function

# Import data
from tensorflow.examples.tutorials.mnist import input_data

import tensorflow as tf

flags = tf.app.flags
FLAGS = flags.FLAGS
flags.DEFINE_string('data_dir', '/tmp/data/', 'Directory for storing data')

mnist = input_data.read_data_sets(FLAGS.data_dir, one_hot=True)

sess = tf.InteractiveSession()

# Create the model
x = tf.placeholder(tf.float32, [None, 784])
W = tf.Variable(tf.zeros([784, 10]))
b = tf.Variable(tf.zeros([10]))
y = tf.nn.softmax(tf.matmul(x, W) + b)
```

### Ruby

``` ruby
require 'finity/event'
require 'finity/machine'
require 'finity/state'
require 'finity/transition'
require 'finity/version'

module Finity
  class InvalidCallback < StandardError; end
  class MissingCallback < StandardError; end
  class InvalidState    < StandardError; end

  # Class methods to be injected into the including class upon inclusion.
  module ClassMethods

    # Instantiate a new state machine for the including class by accepting a
    # block with state and event (and subsequent transition) definitions.
    def finity options = {}, &block
      @finity ||= Machine.new self, options, &block
    end

    # Return the names of all registered states.
    def states
      @finity.states.map { |name, _| name }
    end

    # Return the names of all registered events.
    def events
      @finity.events.map { |name, _| name }
    end
  end

  # Inject methods into the including class upon inclusion.
  def self.included base
    base.extend ClassMethods
  end
end
```

### XML

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mainTag SYSTEM "some.dtd" [ENTITY % entity]>
<?oxygen RNGSchema="some.rng" type="xml"?>
<xs:main-Tag xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <!-- This is a sample comment -->
  <childTag attribute="Quoted Value" another-attribute='Single quoted value'
      a-third-attribute='123'>
    <withTextContent>Some text content</withTextContent>
    <withEntityContent>Some text content with &lt;entities&gt; and
      mentioning uint8_t and int32_t</withEntityContent>
    <otherTag attribute='Single quoted Value'/>
  </childTag>
  <![CDATA[ some CData ]]>
</main-Tag>
```
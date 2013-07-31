
# laser.js

> Laser-precision animation sequencing & timing

### Why?

  * **Precise Sequencing**
  * **Rewind**, **Pause**, and **Resume** Sequence
  * **Automatic jQuery Element caching**
  * **CSS3 Animations**
  * **Event Emitter based** vs. callback approach
  * Debugging option with millisecond count

### Tested Compatibility:

  * **IE10+**
  * **Chrome 27+**
  * **Safari 6+**
  * **Firefox 21+**

### Usage

**_JavaScript_**

```javascript

$(function() {

  'use strict';

  // create new sequence with logging (DEBUG : true)
  var demoSequence = new Laser({
    DEBUG : true
  })

  // on complete log id of completed animation
  .on('animation:completed', function(animation) {
    this.log('completed animation %s', animation.id);
  })
  
  // on complete, rewind
  .on('sequence:completed', function(elapsed) {
    this.rewind();
    this.off('sequence:completed');
  })

  // custom easing method
  .addEasing('bounceOut', 'cubic-bezier(.33,1.66,.08,-1.71)')

  // add animations to sequence
  .add('.box', { left : 500 }, { duration : 750, when : 500  })
  .add('.box', { top  : 250 }, { duration : 750, when : 1250 })
  .add('.box', { left : 50  }, { duration : 750, when : 2000 })
  .add('.box', { top  : 50  }, { duration : 750, when : 2750 })

  // assign a name for debugging
  .name('demo')

  // display event triggers in view
  .on('sequence:started', function() {
    $('.current').text('started');
  })
  
  .on('sequence:completed', function() {
    $('.current').text('completed');
  })
  
  .on('sequence:rewinding', function() {
    $('.current').text('rewinding');
  })

  .on('sequence:paused', function() {
    $('.current').text('paused');
  })

  // play sequence
  demoSequence.play();

});
```

**_HTML_**

```html

<div class="box"></div>

```

**_CSS_**

```css

.box {
  top: 50px;
  left: 50px;
  width: 50px;
  height: 50px;
  position: absolute;
  background-color: #ff0099;
}

```

**Please see _examples_ for a full working example**

```bash
$ bower install
```

### Brought to you by:

  * **@edwardhotchkiss (CandidBlend, LLC)**
  * **@lindseymysse**

### License (MIT)

> Copyright (c) 2013, Edward Hotchkiss


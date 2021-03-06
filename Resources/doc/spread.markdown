# Spread System

Example, we add action

    Chuck Norris Own the World with Vic Mc Key

We want to publish it on:

* Chuck Norris wall
* Tom wall
* Bazinga Wall
* Francky Vincent Wall

When you publish a timeline action, you can choose spreads by defining Subject Model and Subject Id.

## Defining a Spread class


Create the class:

```php
<?php

namespace Acme\TimelineBundle\Spread;

use Highco\TimelineBundle\Spread\SpreadInterface;
use Highco\TimelineBundle\Spread\Entry\EntryCollection;
use Highco\TimelineBundle\Spread\Entry\Entry;
use Highco\TimelineBundle\Model\TimelineAction;

class MySpread implements SpreadInterface
{
    public function supports(TimelineAction $timelineAction)
    {
        return true; //or false, you can look at timeline action to make your decision
    }

    public function process(TimelineAction $timelineAction, EntryCollection $coll)
    {
        $entry = new Entry();
        $entry->subjectModel = "\MySubject";
        $entry->subjectId = 1;

        //OR

        $entry = Entry::create('\MySubject', 1);

        $coll->set('mytimeline', $entry);
    }
}
```

Add it to services


```xml
<service id="my_service" class="MyClass">
    <tag name="highco.timeline.spread"/>
</service>
```

To see which spreads are defined:

```
php app:console highco:timeline-spreads
```

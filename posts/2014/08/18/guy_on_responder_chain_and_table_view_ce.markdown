@title Guy on Responder Chain and Table View Cells
@pubDate 2014-08-18 10:51:30 -0700
@modDate 2014-08-18 18:01:31 -0700
Guy English says <a href="http://kickingbear.com/blog/archives/472">not to wire up buttons in table view cells to first responder</a>:

>If I find a UIButton tossing some message up the responder chain, documented nowhere else except in the Interface Builder UI? That sucks. Do you think I’m being funny?

I’ve done this myself. Possibly even often. (Though it’s likely I wired it up in code rather than in IB.)

The thing is: I want the enclosing view controller to get the action message. When something needs to happen — changing the model, presenting another view controller, etc. — it’s likely that it’s something the view controller should do. Table view cells shouldn’t have that kind of power.

Guy writes:

>Simply sending a message up the responder chain that some sub-item of a view has been tapped doesn’t help make the user’s intention clear except under the most superficial or specifically co-ordinated conditions.

My cases may be superficial. I expect the message only to go as far as the nearest view controller, and the only things it needs in order to know what to do are the message itself and the button that triggered it (the sender).

(If you have the button, you can find out what cell it’s in, get the index path of that cell, then look up what model object it refers to. Which sounds like a pain but actually isn’t.)

I think, though, that it’s likely I’m doing this in cases where I’m not using IB, since there’s no way to wire up the action to the view controller in code without somehow giving the table view cell a reference to the view controller, which I don’t want to do.

Is it possible in IB to wire up a button in a cell to an action method in the enclosing view controller? I would think so. (Memory is hazy on this.) If so, being explicit like that is probably a good thing, especially for the sake of the next person to look at the project.

But there’s a case that worries me: table view cells may be reused in different view controllers. In that case, I think you *do* want to wire up actions to first responder. (But then document them in the code, so Guy doesn’t have to go crazy.)

There’s a small case like that in Vesper: the Typography settings screen has a text preview feature, and that table view cell is the same table view cell used in the timeline.

(However, there are no buttons and no actions in this case, and so the issue of action targets doesn’t actually come up.)

<p style="text-align:center">* * *</p>

<i>Update 4:45 pm:</i> Well, Guy’s right. The way you should do it is to create a protocol that the view controller conforms to. The cell’s delegate is the view controller.

(This way the cell doesn’t need to know about a specific class of view controller: it just needs to know about that protocol. I have real-life cases where a specific UITableViewCell subclass is used by different classes of view controllers.)

The button should be wired to an action method in the cell. That action method should call the right method on the cell’s delegate.

It’s likely, in this scenario, that you also want the cell to have a reference to a model object. I myself would make this opaque — the cell could have an <code>id representedObject</code> property, which is set when the view controller configures the cell.

This way, inside an action method in the cell, to actually do the thing, you’d have code like this:

<code>[self.delegate doAThingWithAModelObject:&#8203;self.&#8203;representedObject];</code>

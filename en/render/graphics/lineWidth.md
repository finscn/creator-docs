# LineWidth

Use `lineWidth()` method to add a new point, and then create a line from that point to the last specified point in the canvas.

| Parameter | description
| -------------- | ----------- |
| number | The width of the current line, in pixels.

## example

```javascript
var ctx = node.getComponent(cc.Graphics);
ctx.lineWidth = 20;
ctx.rect(20,20,80,100);
ctx.fill();
```

<a href="graphics/lineWidth.png"><img src="graphics/lineWidth.png"></a>

<hr>

Return to [Graphics Component Reference](../../components/graphics.md).

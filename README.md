Each custom PIXI.js build will include the minimum necessary number of dependencies. Moreover,  these dependencies are included by default in the list, so you can not untick them from the bundle code.


```html
<!DOCTYPE html>
<html lang="en">
 
<head> 
    <script src="https://pixijs.download/dev/packages/constants.min.js"></script>
    <script src="https://pixijs.download/dev/packages/math.min.js"></script>
    <script src="https://pixijs.download/dev/packages/runner.min.js"></script>
    <script src="https://pixijs.download/dev/packages/settings.min.js"></script>
 
    <script src="https://pixijs.download/dev/packages/ticker.min.js"></script>
     <!-- Big chunk of code -->
    <script src="https://pixijs.download/dev/packages/utils.min.js"></script>
	  <!-- Includes Filter, Texture, Renderer, BatchRender etc… -->
    <script src="https://pixijs.download/dev/packages/core.min.js"></script>
</head>
 
<body>
    <script>
        PIXI.Renderer.registerPlugin('batch', PIXI.BatchRenderer);
    </script>
</body>
</html>
```





You do not have that functionality you used to yet, so you have to add a few more dependencies to use the Application class and register the Ticker.
```html
    <!-- Has Bounds, DisplayObject, Container, etc...  -->
    <script src="https://pixijs.download/dev/packages/display.min.js"></script>
    <!-- has Application and ResizePlugin classes -->
    <script src="https://pixijs.download/dev/packages/app.min.js"></script>
</head>
 
<body>
    <script>
        PIXI.Renderer.registerPlugin('batch', PIXI.BatchRenderer);
        // register ticker plugin
        PIXI.Application.registerPlugin(PIXI.TickerPlugin); 
        // we have the Application with its canvas    
        const app = new PIXI.Application();
        document.body.appendChild(app.view);
        // we have the ticker 
        app.ticker.add((delta) => {
            console.log(delta);
        });
    </script>
</body>
 
</html>
```
 
At this point, you have a very basic application you used to. Now, you can create Containers, push them to the stage, resize canvas view, add your hooks to the ticker, use the ticker, and track time.
From now on, you can add more dependencies based on your needs.  Let’s see a few more examples.

### How to add and use PIXI Sprites.
The application dependencies which are described above can be extended with the Sprite class. That will allow us to use Sprites to render textures which, in turn, wraps the source images.

```html 
   <!-- Add part that has the Sprite class -->
<script src="https://pixijs.download/dev/packages/sprite.min.js"></script>
</head>
 
<body>
    <script>
        PIXI.Renderer.registerPlugin('batch', PIXI.BatchRenderer);
        // register ticker plugin
        PIXI.Application.registerPlugin(PIXI.TickerPlugin);
        // we have the Application with its canvas    
        const app = new PIXI.Application();
        document.body.appendChild(app.view);
        // will create an empty sprite (uses Texture.EMPTY)
        const sprite = new PIXI.Sprite();
        app.stage.addChild(sprite);
    </script>
</body>
 
</html>
```
	
But empty sprites are not what we need, right?. You can use Containers to group content instead. To create a sprite with a texture, we need to load a picture and wrap that image within a Texture. Then you pass the texture to the sprite.
In both examples below a texture will be created which loads a picture. In other words there will be a “GET” request  to fetch a picture, so you have to make sure you host your files.

```javascript
      // create a texture for sprite
        const logoTexture = PIXI.Texture.from("./path_to_your_image.png");
        const icon = new PIXI.Sprite(logoTexture);
        app.stage.addChild(icon);
 
        // or you can use the static method of Sprite
        const icon2 = PIXI.Sprite.from("./path_to_your_image.png");
        app.stage.addChild(icon2);
``` 


### How to add and use PIXI Text

Let's look at this scenario where you are going to work only with text. One more dependency has to be added to all dependencies above, which is Text. Also you can see we include sprite as well. That is because PIXI Text extends PIXI Sprite. Moreover, when a text is being created, a new Texture of this text will be created and will be passed to the Sprite as the texture to render.



```html
     <!-- Add part that has the Sprite class -->
  <script src="https://pixijs.download/dev/packages/sprite.min.js"></script>
    <!--  Has TextMetrics, TextStyle and Text   -->
    <script src="https://pixijs.download/dev/packages/text.min.js"></script>
</head>
 
<body>
    <script>
 
        PIXI.Renderer.registerPlugin('batch', PIXI.BatchRenderer);
        // register ticker plugin
        PIXI.Application.registerPlugin(PIXI.TickerPlugin);
        // we have the Application with its canvas    
        const app = new PIXI.Application();
        document.body.appendChild(app.view);
 
        // to create the style for a text, or you can use
        // https://pixijs.io/pixi-text-style/#
        const styles = new PIXI.TextStyle({
            fill: "#e65b5b",
            fontFamily: "Arial Black",
            fontStyle: "italic",
            fontWeight: "lighter",
            padding: 20
        });
        // create the text
        const text = new PIXI.Text("PIXI.js", styles);
        app.stage.addChild(text);
 
    </script>
</body>
 
</html>
```



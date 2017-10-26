## Environment setup

This is only required to access the video stream, so does not need to be done right away

1. download NPM and node.js - https://www.npmjs.com/get-npm
2. download iTerm - https://www.iterm2.com/
3. open iterm and download nodemon by typing `npm install nodemon -g` in the command line
4. Within the terminal, navigate to the file path with the project in it - https://computers.tutsplus.com/tutorials/navigating-the-terminal-a-gentle-introduction--mac-3855
5. within that path, run `nodemon index.js` - note you will need the same file structure as the other project, eg. an `index.js` file (you should just cope the other one) and a `index.html` file
6. Once you have run that, open `http://localhost:8000/` in chrome

## Main tasks

### markup

You need to build all your HTML and CSS framework. For this part you can just use an empty `<div></div>` element to act represent your canvas.

### embedding the canvas and video tags

Once your HTML and CSS are looking right, you can add a `<canvas></canvas>` and `<video></video>` tag into your markup, with these elements, you usually set the width and height as valued on the elements, eg. `<canvas width="100" height="100"></canvas>`. You should also give these elements an `id` so we can target it with the javascript, eg. `<canvas id="myCanvis" width="100" height="100"></canvas>`.

You also need to do some fancy styling to get these elements to be on top of each other, you can do this by setting one of them to `position: absolute`. The only thing to remember is, absolute positioning is relative to the first parent with a `position: relative` style. That might be confusing, but it just means that the div that is wrapping those elements needs that css definition. eg. 
```
    <div> <- this div needs position: relative
        <video id="myVideo" width="100" height="100"></video>
        <canvas id="myCanvis" width="100" height="100"></canvas>
    </div>
```
Remember that you need the canvas element to be on top of video element

### Drawing on the canvas

Once you have your canvas in the markup you need to get access to the element in javascript, you can do this by looking it up by it's id and assigning it to a variable. Eg. 
```
    var canvas = document.getElementById("myCanvis");
```

Now that you have it, you need to set up a `context` to draw on. So add that code below
```
    var canvas = document.getElementById("myCanvis");
    var context = canvas.getContext("2d");
```

Btw, you can check if your variables are correct by logging them to the console and seeing what is assigned to them. eg.
```
    var canvas = document.getElementById("myCanvis");
    console.log(canvas)
    var context = canvas.getContext("2d");
    console.log(context)
```
if you see `undefined`, it means that you you didn't assign anything, so you probably couldn't find the element. It's probably because the id was wrong

You should look at some canvas tutorials to get an idea of how to use it:
- https://www.udacity.com/course/html5-canvas--ud292?gclid=CjwKCAjw7MDPBRAFEiwAppdF9GyC7d6imm2SsrfzgP0Z-_rbELeju-z3aMJVpnYtLWub54ADe0xXDBoCrtkQAvD_BwE
Or just search youtube.

### creating the video stream

For this part, I would probably just copy the code I wrote, it's such a small part of the project, you don't really need to understand it too well.

But essentially, you need to get access to the webcam, the target the video element on the page, and set the source to the webcam, then tell it to start playing. eg. (not compete example)
```
    var video = document.getElementById("video");

    ...

    video.src = window.URL.createObjectURL(stream);
    video.play();
```

### taking a picture and analysing it

When everything is set up, painting a picture to the canvas is easy. It's just 
```
context.drawImage(video, 0, 0, canvas.width, canvas.height)
```
You will need to nest this within an event listener, so you can control when it happens.

And getting pixel data can be done using
```
    var pixel1 = context.getImageData(x, y, 1, 1).data
    
    // to look at it 👇
    console.log(pixel1)
```

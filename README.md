***
# Today-I-learned
[a link to section](f)
</br>
<a href='#the_destination'>Link to the destination22222'</a>
> In this file I am going to write all useful codes that I have learned during my coding. Having them helps me to fresh my memory by looking at the codes.
```
damadi
```
<!DOCTYPE html>
<html>
<body>

<h1>My First Heading</h1>

<p>My first paragraph.</p>

<div class="split left">
  <div class="centered">
    <h2>Jane Flex</h2>
    <p>Some text.</p>
  </div>
</div>

<div class="split right">
  <div class="centered">
    <h2>John Doe</h2>
    <p>Some text here too.</p>
  </div>
</div>

.split {
  height: 100%;
  width: 50%;
  position: fixed;
  z-index: 1;
  top: 0;
  overflow-x: hidden;
  padding-top: 20px;
}


.left {
  left: 0;
  background-color: #111;
}


.right {
  right: 0;
  background-color: red;
}


.centered {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
}


.centered img {
  width: 150px;
  border-radius: 50%;
}

</body>
</html>

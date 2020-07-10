<!DOCTYPE html>
<html lang="en" >
<head>
  <meta charset="UTF-8">
  <title>Gregor J.</title>
  <style>
    .var-highlight {
  color: purple;
  font-weight: bold;
}

.string-highlight {
  color: red;
}

#typewriter {
  font-size: 2em;
  margin: 0;
  font-family: "Courier New";
}
#typewriter:after {
  content: "|";
  -webkit-animation: blink 500ms linear infinite alternate;
          animation: blink 500ms linear infinite alternate;
}

@-webkit-keyframes blink {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
@keyframes blink {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
</style>

</head>
<body>
<!-- partial:index.partial.html -->
<pre id="typewriter">
  I am a <span class="string-highlight">web developer</span>: HTML5, CSS3, PHP, JavaScript.

  I am a <span class="string-highlight">software developer</span>: C# / .NET

  By day I am a <span class="string-highlight">BI Consultant</span>.
  By night I work on my degree in <span class="string-highlight">Information Technology</span>.

  I am a big fat <span class="var-highlight">nerd</span>, and I love cats.

</pre>
<!-- partial -->
  <script>
    function setupTypewriter(t) {
      var HTML = t.innerHTML;

      t.innerHTML = "";

      var cursorPosition = 0,
          tag = "",
          writingTag = false,
          tagOpen = false,
          typeSpeed = 100,
        tempTypeSpeed = 0;

      var type = function() {
        
          if (writingTag === true) {
              tag += HTML[cursorPosition];
          }

          if (HTML[cursorPosition] === "<") {
              tempTypeSpeed = 0;
              if (tagOpen) {
                  tagOpen = false;
                  writingTag = true;
              } else {
                  tag = "";
                  tagOpen = true;
                  writingTag = true;
                  tag += HTML[cursorPosition];
              }
          }
          if (!writingTag && tagOpen) {
              tag.innerHTML += HTML[cursorPosition];
          }
          if (!writingTag && !tagOpen) {
              if (HTML[cursorPosition] === " ") {
                  tempTypeSpeed = 0;
              }
              else {
                  tempTypeSpeed = (Math.random() * typeSpeed) + 50;
              }
              t.innerHTML += HTML[cursorPosition];
          }
          if (writingTag === true && HTML[cursorPosition] === ">") {
              tempTypeSpeed = (Math.random() * typeSpeed) + 50;
              writingTag = false;
              if (tagOpen) {
                  var newSpan = document.createElement("span");
                  t.appendChild(newSpan);
                  newSpan.innerHTML = tag;
                  tag = newSpan.firstChild;
              }
          }

          cursorPosition += 1;
          if (cursorPosition < HTML.length - 1) {
              setTimeout(type, tempTypeSpeed);
          }

      };

      return {
          type: type
      };
  }

  var typer = document.getElementById('typewriter');

  typewriter = setupTypewriter(typewriter);

  typewriter.type();
  </script>

</body>
</html>



<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Interactive IB Letter</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #f4f4f8;
      color: #333;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      min-height: 100vh;
      align-items: center;
    }
    #chatbox {
      width: 90%;
      max-width: 600px;
      background: white;
      padding: 2rem;
      border-radius: 12px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
      overflow-y: auto;
      max-height: 80vh;
    }
    .message {
      margin: 1rem 0;
    }
    .bot {
      font-weight: 500;
    }
    .user {
      font-weight: bold;
      text-align: right;
      color: #0077cc;
    }
    .options {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 10px;
    }
    button {
      padding: 0.5rem 1rem;
      border: none;
      border-radius: 8px;
      background-color: #0077cc;
      color: white;
      cursor: pointer;
      transition: background 0.2s ease;
    }
    button:hover {
      background-color: #005fa3;
    }
  </style>
</head>
<body>
<div id="chatbox"></div>

<script>
  const chatbox = document.getElementById('chatbox');

  const steps = [
    { 
      message: "Dear future IB student,\nI'm going to start off with a strong (and maybe even controversial) claim: English was my favorite class in CEGEP.",
      next: () => askRScore()
    }
  ];

  let currentStep = 0;

  function appendMessage(text, sender = 'bot') {
    const div = document.createElement('div');
    div.className = 'message ' + sender;
    div.innerText = text;
    chatbox.appendChild(div);
    chatbox.scrollTop = chatbox.scrollHeight;
  }

  function askRScore() {
    appendMessage("How do you feel about the R-score?");
    showOptions([
      { text: "I'm anxious", action: rscoreAnxious },
      { text: "I don’t know what that is", action: rscoreIgnorant },
      { text: "Who cares?!", action: rscoreRebel }
    ]);
  }

  function rscoreAnxious() {
    appendMessage("I'm anxious", 'user');
    appendMessage("I hear you, I was terrified as well! It seems as though this one mysterious formula determines your entire future!");
    reflectOnRScore();
  }

  function rscoreIgnorant() {
    appendMessage("I don’t know what that is", 'user');
    appendMessage("I'm certain you'll soon learn everything about it. IB students REALLY value it (but we are more than that)!");
    reflectOnRScore();
  }

  function rscoreRebel() {
    appendMessage("Who cares?!", 'user');
    appendMessage("Ok, hold on, are you even an IB student? 😄 As long as you're saying this because you understand that the R-score doesn’t define you, you’re on the right path!");
    reflectOnRScore();
  }

  function reflectOnRScore() {
    appendMessage("While it seems like CEGEP is all about the R-score, I've learnt that it's way more than that; it’s about the classmates that become your best friends, the novels you read that become your favorite books, the club you join that helps you find your passion.");
    appendMessage("And if you put everything you’ve got into everything you do, you won’t even have to worry about your R-score!");
    setTimeout(() => askReadingStyle(), 500);
  }

  function askReadingStyle() {
    appendMessage("How do you read?");
    showOptions([
      { text: "I annotate heavily", action: readingAnnotate },
      { text: "I just highlight", action: readingHighlight },
      { text: "SparkNotes + ChatGPT", action: readingSparknotes }
    ]);
  }

  function readingAnnotate() {
    appendMessage("I annotate heavily", 'user');
    appendMessage("That’s great! There’s never enough color! Keep a sheet or doc with key quotes too—you’ll thank yourself later.");
    setTimeout(() => askCreativity(), 500);
  }

  function readingHighlight() {
    appendMessage("I just highlight", 'user');
    appendMessage("Nice! Highlighting is solid, but jot down key passages too—you’ll use them again.");
    setTimeout(() => askCreativity(), 500);
  }

  function readingSparknotes() {
    appendMessage("SparkNotes + ChatGPT", 'user');
    appendMessage("Yeah, that won’t work in IB! Use those tools to get a rough idea, but you’ll have to do the real thinking yourself!");
    setTimeout(() => askCreativity(), 500);
  }

  function askCreativity() {
    appendMessage("Another reason I love English: it’s one of the rare IB classes where you get to be creative! What are you into?");
    showOptions([
      { text: "Music", action: passionMusic },
      { text: "Writing/Poetry", action: passionWriting },
      { text: "Anything else", action: passionOther }
    ]);
  }

  function passionMusic() {
    appendMessage("Music", 'user');
    appendMessage("Great! Write a song from a character’s perspective or compose a score for a scene. Make it yours!");
    wrapUp();
  }

  function passionWriting() {
    appendMessage("Writing/Poetry", 'user');
    appendMessage("Well, you’re in the right class! Let the words flow and unleash your inner Shakespeare!");
    wrapUp();
  }

  function passionOther() {
    appendMessage("Anything else", 'user');
    appendMessage("Whether it's photography, coding, sports, or film—find a way to bring your passions into your portfolio. Creative = high marks!");
    wrapUp();
  }

  function wrapUp() {
    appendMessage("One last thing—English lets us tackle real-world issues: feminism, identity, mental health, and more. Language reflects culture and can spark deep conversations.");
    appendMessage("All in all, English A will only be fun if you give it a real chance. Read the books, speak up in class, and dive deep into the ideas.");
    appendMessage("Who knows, you might fall in love with it too.");
    appendMessage("—A fellow IB survivor :)");
  }

  function showOptions(options) {
    const container = document.createElement('div');
    container.className = 'options';
    options.forEach(opt => {
      const btn = document.createElement('button');
      btn.textContent = opt.text;
      btn.onclick = () => {
        container.remove();
        opt.action();
      };
      container.appendChild(btn);
    });
    chatbox.appendChild(container);
    chatbox.scrollTop = chatbox.scrollHeight;
  }

  // Start it up
  steps[0].next();
</script>
</body>
</html>

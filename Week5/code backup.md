let flag = 0,
  Arrowflag = 0;
let bodies_array = [];
let rad = 5;
let lim = 40;

let planets = [];
let rock, bg;

function preload() {
  // let img1 = loadImage("assets/1.png");
  //   planets.push(img1);
  
  let img2 = loadImage("assets/2.png");
      planets.push(img2);

  let img3 = loadImage("assets/3.png");
      planets.push(img3);

  let img4 = loadImage("assets/4.png");
      planets.push(img4);
  

//   let img5 = loadImage("assets/5.png");
//       planets.push(img5);

//   let img6 = loadImage("assets/6.png");
//       planets.push(img6);

  // let img7 = loadImage("assets/7.png");
  rock = loadImage("assets/rock.png");  
  
  // bg = loadImage ("assets/starsbg.jpg");
}

class Body {
  constructor(x, y, rad, vel, type) {
    this.pos = createVector(x, y);
    //make mass dynamic
    this.mass = Math.pow(rad, 2.5) / 4;
    // this.G = G
    this.vel = vel;
    this.acc = createVector(0, 0);
    this.force = createVector();
    // Radius of sphere
    this.r = rad;
    this.type = type;

    if (rad <= 5) {
      this.image = rock;
    } else {
      // print(planets[Math.floor(Math.random()*planets.length)]);
      this.image = planets[Math.floor(Math.random() * planets.length)];
    }
    // print(this.r)
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acc.add(f);
  }

  attract(Body) {
    let force = p5.Vector.sub(this.pos, Body.pos);
    // let distanceSq = force.magSq();
    let distanceSq = constrain(force.magSq(), 10, 1000);
    let G = 0.05;
    let strength = (G * (this.mass * Body.mass)) / distanceSq;
    force.setMag(strength);
    Body.applyForce(force);
  }

  checkCollision(Body) {
    if (
      this.pos.dist(Body.pos) < this.r / 2 + Body.r / 2 &&
      this.mass >= Body.mass
    ) {
      // print(Body);
      return 1;
    }
  }

  update() {
    if (this.type != "star") {
      this.vel.add(this.acc);
      this.pos.add(this.vel);
      this.acc.set(0, 0);
    }
  }

  show() {
    noStroke();
    fill(79, 113, 255);
    ellipse(this.pos.x, this.pos.y, this.r);
    image(this.image, this.pos.x, this.pos.y, this.r, this.r);
  }
}


let x, y;
let c;
let down;
let stars = [];

function setup() {
  createCanvas(900, 600);
  translate(width / 2, height / 2);
  for (let element of document.getElementsByClassName("p5Canvas")) {
    element.addEventListener("contextmenu", (e) => e.preventDefault());
    imageMode(CENTER);
  }
  
  // Create background with stars
  
  for (let i = 0; i < 1000; i++) {
    stars[i] = new Star(random(width), random(height), random(255), random(0.1, 3), random(1));
  }
  
}

class Star {
  constructor(tx, ty, tc, tf, td) {
    this.x = tx;
    this.y = ty;
    this.c = tc;
    this.f = tf;
    this.down = td;
  }

  showStar() {
    stroke(this.c)
    point(this.x, this.y);
  }
}


function draw() {
  // tint(0, 153, 204, 126);
  // image(bg, width/2, height/2, width, height);
  
  background(0, 50);
  for (let i = 0; i < stars.length; i++) {
    // stars[i].twinkle();
    stars[i].showStar();
  }

  fill(200, 70);
  ellipse(mouseX, mouseY, rad);

  if (flag == 1) {
    if (Arrowflag == 1) {
      temp = p5.Vector.sub(start, createVector(mouseX, mouseY));
      drawArrow(createVector(mouseX, mouseY), temp.limit(lim));
    }
    for (let body of bodies_array) {
      for (let other of bodies_array) {
        if (body !== other) {
          body.attract(other);
          if (body.checkCollision(other)) {
            bodies_array.splice(bodies_array.indexOf(other), 1);
            break;
          }
        }
      }
    }
    for (let body of bodies_array) {
      body.update();
      body.show();
    }
  }
}

function mouseWheel() {
  // print(event.deltaY/125);

  // rad = rad - (event.deltaY/125);
  if (-event.deltaY / 125 > 0) {
    rad = rad + 17.5;
  } else if (-event.deltaY / 125 < 0) {
    rad = rad - 17.5;
  }

  if (rad <= 5) {
    rad = 5;
  }
  if (rad >= 40) {
    rad = 40;
  }
}

function mousePressed() {
  if (mouseButton === LEFT) {
    Arrowflag = 1;
    flag = 1;
    start = createVector(mouseX, mouseY);
  } else if (mouseButton == RIGHT) {
    // print("hello");
  }
}

function mouseClicked() {
  if (mouseButton == LEFT) {
    end = createVector(mouseX, mouseY);

    init_vel = p5.Vector.div(p5.Vector.sub(start, end).limit(lim), 10);
    Arrowflag = 0;
    bodies_array.push(new Body(mouseX, mouseY, rad, init_vel, "planet"));
  }
  // if (mouseButton == RIGHT) {
  //   bodies_array.push(new Body(mouseX, mouseY, 50, createVector(), "star"));
  //   print("s")
  // }
}

function keyPressed() {
  background(0);
  if (keyCode === UP_ARROW) {
    for (let body of bodies_array) {
      body.pos.y += 50;
    }
  } else if (keyCode === DOWN_ARROW) {
    for (let body of bodies_array) {
      body.pos.y += -50;
    }
  } else if (keyCode === RIGHT_ARROW) {
    for (let body of bodies_array) {
      body.pos.x += -50;
    }
  } else if (keyCode === LEFT_ARROW) {
    for (let body of bodies_array) {
      body.pos.x += +50;
    }
  }
}

function drawArrow(base, vec) {
  // print("wprked")
  push();
  stroke(255, 0, 0);
  strokeWeight(3);
  fill(255, 0, 0);
  translate(base.x, base.y);
  line(0, 0, vec.x, vec.y);
  rotate(vec.heading());
  let arrowSize = 7;
  translate(vec.mag() - arrowSize, 0);
  triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
  pop();
}

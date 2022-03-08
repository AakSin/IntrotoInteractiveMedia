//Putting there here because I had a close call and almost deleted the sketch.js while removing some asset files ://///

let flag = 0,
  Arrowflag = 0;
let bodies_array = [];
let rad = 5;
let lim = 40;

let planets = ["1.png", "2.png", "3.png", "4.png", "5.png", "6.png"];
let rock = "rock.png";

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
    
    if (rad>5){
      this.image = "rock.png"
    }
      else {
        this . image = 
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
    
    if (this.type != "star"){
      this.vel.add(this.acc);
      this.pos.add(this.vel);
      this.acc.set(0, 0);
    }
  }

  show() {
    noStroke();
    fill(79, 113, 255);
    ellipse(this.pos.x, this.pos.y, this.r);
  }
}

function setup() {
  createCanvas(900, 600);
  translate(width / 2, height / 2);
  for (let element of document.getElementsByClassName("p5Canvas")) {
    element.addEventListener("contextmenu", (e) => e.preventDefault());
  }
}

function draw() {
  background(0, 50);

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
  if (-event.deltaY/125 > 0)
    {
      rad = rad + 17.5;
    }
  else if (-event.deltaY/125 < 0)
    {
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
  } 
    else if (keyCode === RIGHT_ARROW) {
    for (let body of bodies_array) {
      body.pos.x += -50;
    }
  }
      else if (keyCode === LEFT_ARROW) {
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

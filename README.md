# Ping-pong-game
import turtle as t
# Initialize player scores
player1score = 0
player2score = 0

# Create the main window
window=t.Screen ()
window.title("Ping Pong")
window.bgcolor("green")
window.setup(width=800, height=600)
window.tracer(0)

# Creating left paddle
leftpaddle = t.Turtle()
leftpaddle.speed(0)
leftpaddle.shape("square")
leftpaddle.color("red")
leftpaddle.shapesize(stretch_wid=5, stretch_len=1)
leftpaddle.penup()
leftpaddle.goto(-350, 0)

# Creating right paddle
rightpaddle = t.Turtle()
rightpaddle.speed(0)
rightpaddle.shape("square")
rightpaddle.color("purple")
rightpaddle.shapesize(stretch_wid=5, stretch_len=1)
rightpaddle.penup()
rightpaddle.goto(350, 0)

# Creating ball
ball = t.Turtle()
ball.speed(1)
ball.shape("circle")
ball.color("white")
ball.penup()
ball.goto(0, 0)
ball.dx = 0.2
ball.dy = -0.2

# Functions to move the paddles
def leftpaddle_up():
    y = leftpaddle.ycor()
    if y < 250:
        y += 20
        leftpaddle.sety(y)

def leftpaddle_down():
    y = leftpaddle.ycor()
    if y > -240:
        y -= 20
        leftpaddle.sety(y)

def rightpaddle_up():
    y = rightpaddle.ycor()
    if y < 250:
        y += 20
        rightpaddle.sety(y)

def rightpaddle_down():
    y = rightpaddle.ycor()
    if y > -240:
        y -= 20
        rightpaddle.sety(y)

# Keyboard bindings
window.listen()
window.onkeypress(leftpaddle_up, "w")
window.onkeypress(leftpaddle_down, "s")
window.onkeypress(rightpaddle_up, "Up")
window.onkeypress(rightpaddle_down, "Down")

# Main game loop
while True:
    window.update()

    # Move the ball
    ball.setx(ball.xcor() + ball.dx)
    ball.sety(ball.ycor() + ball.dy)

    # Border checking
    if ball.ycor() > 290:
        ball.sety(290)
        ball.dy *= -1

    if ball.ycor() < -290:
        ball.sety(-290)
        ball.dy *= -1

    if ball.xcor() > 390:
        ball.goto(0, 0)
        ball.dx *= -1
        player1score += 1
        print("Player 1: {}".format(player1score))

    if ball.xcor() < -390:
        ball.goto(0, 0)
        ball.dx *= -1
        player2score += 1
        print("Player 2: {}".format(player2score))

    # Paddle and ball collisions
    if (ball.dx > 0) and (ball.xcor() > 340 and ball.xcor() < 350) and (ball.ycor() < rightpaddle.ycor() + 50 and ball.ycor() > rightpaddle.ycor() - 50):
        ball.setx(340)
        ball.dx *= -1

    elif (ball.dx < 0) and (ball.xcor() < -340 and ball.xcor() > -350) and (ball.ycor() < leftpaddle.ycor() + 50 and ball.ycor() > leftpaddle.ycor() - 50):
        ball.setx(-340)
        ball.dx *= -1


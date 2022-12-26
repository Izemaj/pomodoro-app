
<h2>Building the Pomodoro Timer</h2>
<p>In this tutorial, we will build a Pomodoro timer program using Python and the Tkinter module. The Pomodoro Technique is a time management method that involves working for a set amount of time, taking a short break, and then repeating this process.</p>
<h3>Step 1: Import the necessary modules</h3>
<p>First, we need to import the necessary modules to build the Pomodoro timer. We will use Tkinter to create the user interface (UI) and math to perform some calculations.</p>
<pre><code>from tkinter import *
import math
</code></pre>
<h3>Step 2: Define constants</h3>
<p>Next, we will define some constants for the colors, font, and timer durations. These constants will be used throughout the program to keep the code clean and easy to read.</p>
<pre><code>PINK = "#e2979c"
RED = "#e7305b"
GREEN = "#9bdeac"
YELLOW = "#f7f5dd"
FONT_NAME = "Courier"
WORK_MIN = 25
SHORT_BREAK_MIN = 5
LONG_BREAK_MIN = 20
</code></pre>
<h3>Step 3: Set up the UI</h3>
<p>Next, we will set up the UI of the Pomodoro timer. The UI consists of a canvas to hold the timer display and tomato image, a heading label to display the current state of the timer, a start button to trigger the timer, a reset button to cancel the current timer and reset the counter and check marks, and a check mark display to show the number of completed work periods.</p>
<pre><code>window = Tk()
window.title("Pomodoro")
window.config(padx=100,pady=50,bg=YELLOW)

canvas = Canvas(width=200 , height =224,bg=YELLOW,highlightthickness=0)
tomato_img = PhotoImage(file="tomato.png")
canvas.create_image(100,112, image=tomato_img)
timer_text = canvas.create_text(105,130, text="00:00", fill="white", font=(FONT_NAME,30, "bold"))
canvas.grid(row=1, column=1)

heading =Label(text="Timer", font=(FONT_NAME, 35, "bold"), fg=GREEN, bg=YELLOW)
heading.grid(row=0,column=1)

button1 = Button(text="Start",font=(FONT_NAME, 10),command=start_timer)
button1.grid(row=3,column=0)

check_mark = Label(fg=GREEN, bg=YELLOW)
check_mark.grid(row=3, column=1)

button2 = Button(text="Reset",font=(FONT_NAME, 10), command=reset_timer)
button2.grid(row=3,column=2)
</code></pre>

<h3>Step 4: Define the timer functions</h3>
<p>Next, we will define the functions that implement the timer mechanism. The Pomodoro timer consists of work periods, short breaks, and long breaks. The length of these periods is defined by the constants we defined earlier. The timer mechanism is implemented using the following functions:</p>

<h4>reset_timer</h4>
<pre><code>def reset_timer():
    global reps
    window.after_cancel(timer)
    heading.config(text="Timer", fg=GREEN)
    canvas.itemconfig(timer_text, text="00:00")
    reps = 0
    check_mark["text"] = ""
</code></pre>

<h4>start_timer</h4>
<pre><code>def start_timer():
    global reps
    reps += 1
    work_sec = WORK_MIN
    short_break = SHORT_BREAK_MIN
    long_break = LONG_BREAK_MIN

    if reps % 8 == 0:
        countdown(long_break)
        heading.config(text="Break", fg=RED)
    elif reps % 2 == 0:
        countdown(short_break)
        heading.config(text="Break", fg=PINK)
    else:
        countdown(work_sec)
        heading.config(text="Work", fg=GREEN)
</code></pre>

<h4>countdown</h4>
<pre><code>def countdown(count):
    count_min = math.floor(count/60)
    count_sec = count % 60
    if count_sec < 10:
        count_sec = f"0{count_sec}"
    canvas.itemconfig(timer_text, text = f"{count_min}:{count_sec}")
    if count > 0:
        global timer
        timer = window.after(1000, countdown, count -1)
    else:
        if reps % 2 == 0:
            global marks
            marks += 1
            check_mark["text"] = "✔" * counter
        start_timer()
</code

<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.13/css/all.css" integrity="sha384-DNOHZ68U8hZfKXOrtjWvjxusGo9WQnrNx2sqG0tfsghAvtVlRW3tvkXWZh58N9jp" crossorigin="anonymous">
<h1 class="title">Elixir</h1>

---

<h4>The Erlang Stack</h4>

<img src="./img/erlang_stack.png" height=500px></img>


<span class="didyouknow"><i class='fas fa-info-circle'></i>BEAM = Bogdan/Björn's Erlang Abstract Machine</span>
<span class="didyouknow"><i class='fas fa-info-circle'></i>OTP = Open Telecom Platform</span>

---

<div class="left half">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/04/Erlang_logo.svg/1200px-Erlang_logo.svg.png" height=100px style="background:white"/><br>
    Created in 1987 by Ericsson<br>
    <br>
    Latest Version : 20.2 (December 2017)
</div>

<div class="right half">
    <img src="https://upload.wikimedia.org/wikipedia/commons/9/92/Official_Elixir_logo.png" height=100px style="background:white"/><br>
    Created in 2012 by José Valim Hernàndez<br>
    <br>
    Latest Version : 1.6.5 (May 2018)
</div>

---

<h4 class="title">The Erlang Core Principles</h4>

<p class="t">
<span class="hl title">Functional Programming</span><br>
See above.
<br><br>
<span class="hl title">Strong, dynamic, typing</span><br>
See above.
<br><br>
<span class="hl title">Actor Model</span><br>
Actors are independent processes that have their own code, data and state.
<br><br>
<span class="hl title">OTP</span><br>
This "standard library" is built around the core ideas of <b>concurrency, fault tolerance and distribution</b>.
</p>

---

<h4 class="title">Actor Model</h4>

Normal functional programs :

<img src="./img/functional_model.png" height=500px></img>

---

<h4 class="title">Actor Model</h4>

Erlang :

<img src="./img/erlang_mode.png" height=500px></img>

---

<h4 class="title">Actor Model</h4>

Actors have lifcecycles

<img src="./img/actor_lifecycle.png" height=500px></img>

---

<h4 class="title">Actor Model</h4>

Actors have supervisors

<img src="./img/supervisor.png" height=500px></img>

---

<h4 class="title">Actor Model</h4>

Supervisors have supervisors

<img src="./img/supervisor2.png" height=500px></img>

---

<h4 class="title">Actor Model</h4>

<br>

<p class="t" style="padding-left:300px;">
"Erlang was designed for<br>
wiriting concurrent programs<br>
that run <b class="hl">forever</b>."<br>
</p>
<i style="font-size:0.6em !important;right:150px;position:absolute;">A History of Erlang - Joe Amstrong</i>

<br>

<small>
With Erlang, Ericsson managed to get a switch to 9-nines availability.<br>
That is less than 1s downtime over 20 years.
</small>

---

<h4 class="title">OTP</h4>

<br>

OTP is a large library that implement<br> <b class="hl">behaviours</b> that can be<br>
reused to write Erlang code.

---

<h4 class="title">Elixir</h4>

<br>

Elixir is just a new syntax over Erlang.<br>

---

https://wandbox.org/  
https://github.com/eXenon/fp-presentation

---

Hello, world !

```
defmodule MyFirstModule do
    def myfirstfunction() do
        IO.puts "Hello, world !"
    end
end

MyFirstModule.myfirstfunction
```

---

Pattern matching is very common in FP.<br>
Elixir has special syntax to use it in functions :

```
defmodule Users do
    def login("alice", "al1c3s3cure"):
        IO.puts "Welcome, Alice !"
    end
    def login("bob", "b0bs3cure"):
        IO.puts "Welcome, Bob !"
    end
    def login(_, _):
        IO.puts "Unknown user or bad password..."
    end
end
```

---

Functional programming is, well, a lot of functions.<br>
The pipe operator allows to chain functions :

```
defmodule Operations do
    def op1(a) do
        String.downcase(a)
    end
    def op2(a, b) do
        a <> b
    end
end

"FOO" |> Operations.op1 |> Operations.op2("bar") |> IO.puts
```

---

Elixir is just a syntax over Erlang.<br>
This means every Erlang library is available :

```
defmodule Wait do
    def long_calculation() do
        :timer.sleep(3000)
    end
end
```
<span class="didyouknow"><i class='fas fa-info-circle'></i>Notice how Wandbox times out at 5 seconds</span>

---

But the best part of the BEAM are still the threads :

```
defmodule Wait do
    ...
end

task1 = Task.async(fn -> Wandbox.hello end)
task2 = Task.async(fn -> Wandbox.hello end)
Task.await(task1)
Task.await(task2)
```

---

Messaging system :

```
defmodule Actor do
    def listen() do
        IO.puts "Waiting for messages..."
        receive do
            "hello" -> IO.puts "Hi there !"
                       listen
            "bye" -> IO.puts "Bye !"
        end
    end
end

pid = spawn fn -> Actor.listen end
send pid, "hello"
send pid, "bye"
```

---

Thinking in processes :<br>
- A web session is a process
- A shopping cart is a process
- Every element in a game is a process

---

A rich ecosystem :

<small class="t">
<p class="hl">Mnesia</p>
Database on the BEAM<br>
<br>
<p class="hl">ETS</p>
Redis on the BEAM<br>
<br>
<p class="hl">Phoenix</p>
NGINX & Ruby on Rails on the BEAM<br>
<br>
</small>

---

<h2>Conclusion</h2>

Functional programing helps thinking about problems.
But it is rarely sufficient and is best used in combination with imperative.<br>
<br>
A functional core, with an imperative shell.

---

<h4 class="title">Questions ?</h4>

---

<h6 class="title">Further material</h6>

<div class="left half t">
<p class="hl">Books</p>
- Programming Elixir<br>
- Hands on Haskell<br>
- Elements of Clojure<br>
- Category Theory for Programmers
<br>
<br>
<p class="hl">Tutorials</p>
- Elixir Docs<br>
- Elixir Etudes by O'Reilly<br>
- Elm/Phoenix by Pragmatic Studio
</div>

<div class="right half t">
<p class="hl">Podcasts</p>
- Lambda Cast<br>
- Elm Town<br>
- Reason Town<br>
- Functional Geekery
<br>
<br>
<p class="hl">Talks</p>
- FP by John Carmack<br>
- Effective Programs by Rich Hickey<br>
- Functional Core, Imperative Shell by DAS<br>
</div>

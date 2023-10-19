# ghostbusters

## How do I take input from the terminal?

### C Sharp

```cs
using System;

class Program
{
    static void Main()
    {
        string name;
        int age;

        // Prompt the user for their name
        Console.Write("Enter your name: ");
        name = Console.ReadLine();

        // Prompt the user for their age
        Console.Write("Enter your age: ");
        if (int.TryParse(Console.ReadLine(), out age))
        {
            // Input was a valid integer
            Console.WriteLine($"Hello, {name}! You are {age} years old.");
        }
        else
        {
            // Input was not a valid integer
            Console.WriteLine("Invalid age input.");
        }
    }
}

```

### Python

```python
# Prompt the user for their name
name = input("Enter your name: ")

# Prompt the user for their age
age = input("Enter your age: ")

# Check if the age input is a valid integer
if age.isdigit():
    # Input is a valid integer
    print(f"Hello, {name}! You are {age} years old.")
else:
    # Input is not a valid integer
    print("Invalid age input.")

```

### Powershell

```powershell
# Prompt the user for their name
$name = Read-Host "Enter your name"

# Prompt the user for their age
$age = Read-Host "Enter your age"

# Check if the age input is a valid integer
if ($age -as [int]) {
    # Input is a valid integer
    Write-Host "Hello, $name! You are $age years old."
} else {
    # Input is not a valid integer
    Write-Host "Invalid age input."
}
```

### Javascript

There is a function in Node form called 'readline', which you **could** use, but I would not recommend it!

Instead, there is a library called prompt-sync, which you can install with ```npm i prompt-sync```

Here is an example of both, for completeness:

#### readline

```js
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

rl.question('Enter your name: ', (name) => {
  rl.question('Enter your age: ', (age) => {
    // Check if the age input is a valid integer
    if (!isNaN(age)) {
      // Input is a valid integer
      console.log(`Hello, ${name}! You are ${age} years old.`);
    } else {
      // Input is not a valid integer
      console.log('Invalid age input.');
    }

    rl.close();
  });
});
```

#### Prompt-sync

```js
const prompt = require('prompt-sync')();

// Prompt the user for their name
const name = prompt('Enter your name: ');

// Prompt the user for their age
const age = prompt('Enter your age: ');

// Check if the age input is a valid integer
if (!isNaN(age)) {
    // Input is a valid integer
    console.log(`Hello, ${name}! You are ${age} years old.`);
} else {
    // Input is not a valid integer
    console.log('Invalid age input.');
}

```

### Java

```java
import java.util.Scanner;

public class InputExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Prompt the user for their name
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();

        // Prompt the user for their age
        System.out.print("Enter your age: ");
        int age;

        try {
            age = Integer.parseInt(scanner.nextLine());

            // Check if the age input is a valid integer
            if (age >= 0) {
                // Input is a valid integer
                System.out.println("Hello, " + name + "! You are " + age + " years old.");
            } else {
                // Input is not a valid age
                System.out.println("Invalid age input.");
            }
        } catch (NumberFormatException e) {
            // Input is not a valid integer
            System.out.println("Invalid age input.");
        }

        scanner.close();
    }
}

```

### Rust

```rust
use std::io;

fn main() {
    let mut input = String::new();

    // Prompt the user for their name
    println!("Enter your name: ");
    io::stdin()
        .read_line(&mut input)
        .expect("Failed to read line");
    let name = input.trim();

    input.clear(); // Clear the input buffer

    // Prompt the user for their age
    println!("Enter your age: ");
    io::stdin()
        .read_line(&mut input)
        .expect("Failed to read line");

    // Parse the age input as an integer
    let age: Result<i32, _> = input.trim().parse();

    match age {
        Ok(age) if age >= 0 => {
            // Input is a valid integer
            println!("Hello, {}! You are {} years old.", name, age);
        }
        _ => {
            // Input is not a valid integer or is negative
            println!("Invalid age input.");
        }
    }
}

```

### Go

```go
package main

import (
 "bufio"
 "fmt"
 "os"
 "strconv"
 "strings"
)

func main() {
 reader := bufio.NewReader(os.Stdin)

 // Prompt the user for their name
 fmt.Print("Enter your name: ")
 name, _ := reader.ReadString('\n')
 name = strings.TrimSpace(name)

 // Prompt the user for their age
 fmt.Print("Enter your age: ")
 ageStr, _ := reader.ReadString('\n')
 ageStr = strings.TrimSpace(ageStr)

 // Parse the age input as an integer
 age, err := strconv.Atoi(ageStr)
 if err == nil && age >= 0 {
  // Input is a valid integer
  fmt.Printf("Hello, %s! You are %d years old.\n", name, age)
 } else {
  // Input is not a valid integer or is negative
  fmt.Println("Invalid age input.")
 }
}

```

## Okay, now I want to build a visual interface... How do I do that?

### C Sharp - Windows forms

```cs
using System;
using System.Windows.Forms;

class Program
{
    static void Main()
    {
        Application.EnableVisualStyles();
        Application.SetCompatibleTextRenderingDefault(false);

        Form form = new Form();
        form.Text = "User Input Form";

        Label nameLabel = new Label();
        nameLabel.Text = "Enter your name:";
        nameLabel.Location = new System.Drawing.Point(10, 10);
        form.Controls.Add(nameLabel);

        TextBox nameTextBox = new TextBox();
        nameTextBox.Location = new System.Drawing.Point(150, 10);
        form.Controls.Add(nameTextBox);

        Label ageLabel = new Label();
        ageLabel.Text = "Enter your age:";
        ageLabel.Location = new System.Drawing.Point(10, 40);
        form.Controls.Add(ageLabel);

        TextBox ageTextBox = new TextBox();
        ageTextBox.Location = new System.Drawing.Point(150, 40);
        form.Controls.Add(ageTextBox);

        Button submitButton = new Button();
        submitButton.Text = "Submit";
        submitButton.Location = new System.Drawing.Point(10, 70);
        form.Controls.Add(submitButton);

        submitButton.Click += (sender, e) =>
        {
            string name = nameTextBox.Text;
            int age;
            if (int.TryParse(ageTextBox.Text, out age))
            {
                // Process the user input
                MessageBox.Show($"Hello, {name}! You are {age} years old.");
            }
            else
            {
                MessageBox.Show("Invalid age input.");
            }
        };

        Application.Run(form);
    }
}

```

### Javascript - in the browser

#### Vanilla, using the Dojo starter

We need to create an .html file and include a javascript file inside it:

```html

```

```js

```

#### Vanilla, using Vite

#### React, using Vite

### Python - Tkinter

```python
import tkinter as tk

def submit():
    name = name_entry.get()
    age = age_entry.get()
    try:
        age = int(age)
        if age >= 0:
            result_label.config(text=f"Hello, {name}! You are {age} years old.")
        else:
            result_label.config(text="Invalid age input.")
    except ValueError:
        result_label.config(text="Invalid age input.")

# Create the main window
root = tk.Tk()
root.title("User Input Form")

# Name input
name_label = tk.Label(root, text="Enter your name:")
name_label.pack()
name_entry = tk.Entry(root)
name_entry.pack()

# Age input
age_label = tk.Label(root, text="Enter your age:")
age_label.pack()
age_entry = tk.Entry(root)
age_entry.pack()

# Submit button
submit_button = tk.Button(root, text="Submit", command=submit)
submit_button.pack()

# Result label
result_label = tk.Label(root, text="")
result_label.pack()

root.mainloop()

```

### Java - Swing

```java
import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class UserInputForm {
    public static void main(String[] args) {
        JFrame frame = new JFrame("User Input Form");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(300, 200);

        JPanel panel = new JPanel();

        JLabel nameLabel = new JLabel("Enter your name:");
        JTextField nameField = new JTextField(20);

        JLabel ageLabel = new JLabel("Enter your age:");
        JTextField ageField = new JTextField(5);

        JButton submitButton = new JButton("Submit");

        JTextArea resultArea = new JTextArea(5, 20);
        resultArea.setEditable(false);

        submitButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String name = nameField.getText();
                String ageStr = ageField.getText();

                try {
                    int age = Integer.parseInt(ageStr);
                    if (age >= 0) {
                        resultArea.setText("Hello, " + name + "! You are " + age + " years old.");
                    } else {
                        resultArea.setText("Invalid age input.");
                    }
                } catch (NumberFormatException ex) {
                    resultArea.setText("Invalid age input.");
                }
            }
        });

        panel.add(nameLabel);
        panel.add(nameField);
        panel.add(ageLabel);
        panel.add(ageField);
        panel.add(submitButton);
        panel.add(resultArea);

        frame.add(panel);
        frame.setVisible(true);
    }
}

```

### Rust - druid

```rust
use druid::widget::{Button, Column, Label, TextBox};
use druid::{AppLauncher, Data, Env, Lens, LocalizedString, Widget, WidgetExt, WindowDesc};

#[derive(Clone, Data, Lens)]
struct AppState {
    name: String,
    age: String,
    result: String,
}

fn main() {
    let main_window = WindowDesc::new(ui_builder)
        .window_size((300.0, 200.0))
        .title(LocalizedString::new("User Input Form"));

    let initial_state = AppState {
        name: String::new(),
        age: String::new(),
        result: String::new(),
    };

    AppLauncher::with_window(main_window)
        .use_simple_logger()
        .launch(initial_state)
        .expect("launch failed");
}

fn ui_builder() -> impl Widget<AppState> {
    let name_label = Label::new("Enter your name:");
    let name_textbox = TextBox::new()
        .lens(AppState::name)
        .fix_width(150.0)
        .lens(AppState::name);

    let age_label = Label::new("Enter your age:");
    let age_textbox = TextBox::new()
        .lens(AppState::age)
        .fix_width(150.0)
        .lens(AppState::age);

    let submit_button = Button::new("Submit").on_click(|ctx, data: &mut AppState, _env| {
        let name = &data.name;
        let age_str = &data.age;

        if let Ok(age) = age_str.parse::<i32>() {
            if age >= 0 {
                data.result = format!("Hello, {}! You are {} years old.", name, age);
            } else {
                data.result = "Invalid age input.".to_string();
            }
        } else {
            data.result = "Invalid age input.".to_string();
        }
    });

    let result_label = Label::new(|data: &AppState, _env: &Env| data.result.clone());

    Column::new()
        .padding(10.0)
        .spacing(10.0)
        .align_items(druid::widget::Align::Center)
        .add(name_label)
        .add(name_textbox)
        .add(age_label)
        .add(age_textbox)
        .add(submit_button)
        .add(result_label)
}

```

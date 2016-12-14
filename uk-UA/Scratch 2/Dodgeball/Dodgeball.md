* * *

title: Викидайли level: Scratch 2 language: uk-UA stylesheet: scratch embeds: "*.png" materials: ["Club Leader Resources/*","Project Resources/*"]

# Передмова {.intro}

В цьому проекті ви дізнаєтеся, як створити гру-платформер, в якій потрібно буде дістатися кінця рівня ухиляючись від рухомих куль.

<div class="scratch-preview">
  crwMD_Iframe_0 <img src="dodge-final.png" />
</div>

# Крок 1: Рух персонажа {.activity}

Давайте почнемо зі створення персонажа, який зможе рухатись ліворуч й праворуч, а також підніматися вгору по стовпах.

## Завдання для виконання {.check}

+ Створіть новий проект у Скретч та видаліть спрайт кота, так щоб проект став пустим. Онлайн Скретч-редактор за посиланням [jumpto.cc/scratch-new](http://jumpto.cc/scratch-new).

+ Для цього проекту вам необхідна тека "Ресурси проекту", яка містить усі зображення, що можуть знадобитися. Переконайтеся, що ви знайшли цю теку, а якщо ні — запитайте вчителя.
    
    ![screenshot](dodge-resources.png)

+ Використайте для фону малюнок "background.png", або намалюйте власний! Якщо ви вирішите намалювати власний, переконайтеся, що стовпи та платформи будуть різних кольорів, і що в кінці шляху будуть двері (або щось подібне). Нижче показано, як проект має виглядати:
    
    ![screenshot](dodge-background.png)

+ Додайте новий спрайт, який буде вашим персонажем. Буде краще, якщо ви виберете спрайт з декількома костюмами, з яких можна зробити анімацію ходіння.
    
    ![screenshot](dodge-characters.png)

+ Давайте використовувати клавіші зі стрілками для руху персонажа. Коли ви натискаєте стрілку вправо, ви хочете, щоб персонаж повертався праворуч, робив декілька кроків і змінював костюм:
    
    ```blocks
    коли натиснуто ⚑
    завжди
        if <key [стрілка вправо v] pressed? > then
            повернути в напрямку (90 v)
            перемістити на (3) кроків
            наступний образ
        end
    end
```

+ Test out your character by clicking the flag and then holding down the right arrow key. Does your player move to the right? Does your character look like they are walking?
    
    ![screenshot](dodge-walking.png)

+ To move your character to the left, you'll need to add another `if` {.blockcontrol} block inside your `forever` {.blockcontrol} loop, which moves your character to the left. Remember to test your new code, to make sure that it works!

+ To climb a pole, your character should move up slightly whenever the up arrow is pressed and they're touching the correct colour. Add this code inside your character's `forever` {.blockcontrol} loop:
    
    ```blocks
    if < <key [стрілка вгору v] pressed?> and <touching color [#FFFF00] ?> > then
        змінити y на (4)
    end
```

+ Test your character - can you climb the yellow poles and get to the end of your level?
    
    ![screenshot](dodge-test-character.png)

## Збережіть свій проект {.save}

## Виклик: Завершення рівня {.challenge}

Can you add more code to your character, so that they say something `if` {.blockcontrol} they get to the brown door?

![screenshot](dodge-win.png)

## Збережіть свій проект {.save}

# Крок 2: Гравітація і стрибки {.activity}

Давайте зробимо рух вашого персонажа більш реалістичним, додавши гравітацію та навчивши його стрибати.

## Завдання для виконання {.check}

+ You may have noticed that your character can walk off a platform into mid-air. Try to walk off of a platform and see what happens.
    
    ![screenshot](dodge-no-gravity.png)

+ To fix this, let's add gravity to your game. Create a new variable called `gravity` {.blockdata}. You can hide this variable from your stage if you want to.
    
    ![screenshot](dodge-gravity.png)

+ Add this new code block, which sets the gravity to a negative number, and then uses this to repeatedly change your character's y-coordinate.
    
    ```blocks
    коли натиснуто ⚑
    встановити [gravity v] в [-4]
    завжди
       змінити y на (gravity)
    end
```

+ Click the flag, and then drag your character to the top of the stage. What happens? Does the gravity work as you expected?
    
    ![screenshot](dodge-gravity-drag.png)

+ Gravity shouldn't move your character through a platform or a pole! Add an `if` {.blockcontrol} block to your code, so that the gravity only works when your character is in mid-air. The gravity code should now look like this:
    
    ```blocks
    коли натиснуто ⚑
    встановити [gravity v] в [-4]
    завжди
       if < not < <touching color [#0000FF] ?> or <touching color [#FFFF00] ?> > > then
            змінити y на (gravity)
        end
    end
```

+ Test the gravity again. Does your character stop when they are on a platform or a pole? Can you walk off the edge of platforms to the level below?
    
    ![screenshot](dodge-gravity-test.png)

+ Let's also make your character jump when the player presses the space bar. One very easy way to do this is to move your character up a few times, using this code:
    
    ```blocks
    коли натиснуто клавішу [пропуск v]
    повторити (10)
       змінити y на (4)
    end
```

As gravity is constantly pushing your character down by 4 pixels, you need to choose a number greater than 4 in your `change y by (4)` {.blockmotion} block. Change this number until you're happy with the height your character jumps.

+ If you test out this code, you'll notice that it works, but the movement isn't very smooth. To make jumping look smoother, you'll need to move your character by smaller and smaller amounts, until they're not jumping anymore.

+ To do this, create another variable called `jump height` {.blockdata}. Again, you can hide this variable if you prefer.

+ Delete the jumping code you added to your character, and replace it with this code:
    
    ```blocks
    коли натиснуто клавішу [пропуск v]
    встановити [jump height v] в [8]
    repeat until < (jump height) = [0] >
        змінити y на (jump height)
        змінити [jump height v] на (-0.5)
    end
```

This code moves your character up by 8 pixels, then 7.5 pixels, then 7 pixels, and so on, until your character has finished jumping. This makes jumping look much smoother.

+ Change the starting value of your `jump height` {.blockdata} variable and test it until you're happy with the height your character jumps.

## Збережіть свій проект {.save}

## Виклик: Реалістичніші стрибки {.challenge}

Your character is able to jump whenever the spacebar is pressed, even if they're already in mid-air. You can test this by just holding down the spacebar. Can you fix this, so that your character can only jump `if` {.blockcontrol} they're touching a blue platform?

## Збережіть свій проект {.save}

# Крок 3: Уникнення куль {.activity.new-page}

Now that you've got your character moving around, let's add some balls for your character to avoid.

## Завдання для виконання {.check}

+ Create a new ball sprite. You can choose any type of ball you like.
    
    ![screenshot](dodge-balls.png)

+ Resize your ball, so that your character can jump over it. Try jumping over the ball to test it.
    
    ![screenshot](dodge-ball-resize.png)

+ Add this code to your ball:
    
    ![screenshot](dodge-ball-motion.png)
    
    This code creates a new ball clone every 3 seconds. Each new clone moves along the top platform.

+ Click the flag to test this out.
    
    ![screenshot](dodge-ball-test.png)

+ Add more code to your ball sprite, so that they move across all 3 platforms.
    
    ![screenshot](dodge-ball-more-motion.png)

+ Finally, you'll need code for when your character gets hit by a ball! Add this code to your ball sprite:
    
    ```blocks
    коли я починаю як клон
    завжди
       if < touching [Pico walking v] ? > then
           оповістити [hit v]
        end
    end
```

+ You'll also need to add code to your character, to move back to the start when they're hit:
    
    ```blocks
    коли одержую [hit v]
    повернути в напрямку (90 v)
    перемістити в x:(-210) y:(-120)
```

+ Test out your character and see if they go back to the start when they've been hit by a ball.

## Збережіть свій проект {.save}

## Виклик: Випадкові кулі {.challenge}

The balls your character has to dodge all look the same, and always appear every 3 seconds. Can you improve them, so that they:

+ don't all look the same?
+ appear after a random amount of time?
+ are a random size?

![screenshot](dodge-ball-random.png)

## Збережіть свій проект {.save}

# Крок 4: Лазери! {.activity.new-page}

Let's make your game a little harder to complete, by adding lasers!

## Завдання для виконання {.check}

+ Add a new sprite to your game, called 'Laser'. It should have 2 costumes, called 'on' and 'off'.
    
    ![screenshot](dodge-lasers-costume.png)

+ Place your new laser anywhere you like, between 2 platforms.
    
    ![screenshot](dodge-lasers-position.png)

+ Add code to your laser, to make it switch between the 2 costumes.
    
    ```blocks
    коли натиснуто ⚑
    завжди
        змінити образ на [Увімкн v]
        чекати (2) секунд
        змінити образ на [Вимк v]
        чекати (2) секунд
    end
```

If you prefer, you can `wait` {.blockcontrol} a `random` {.blockoperators} amount of time between costume changes.

+ Finally, add code to your laser, so that the 'hit' message is broadcast when the laser touches your character. This code will be the same as the code you added to your ball sprite.
    
    You don't need to add any more code to your character - they already know what to do when they get hit!

+ Test out your game to see if you can get past the laser. Change the `wait` {.blockcontrol} times in your code if the lasers are too easy or too hard.

## Виклик: Більше перешкод {.challenge}

If you think your game is still too easy, you can add more obstacles to your level. You can add anything you like, but here are some ideas:

+ A flying killer butterfly;
+ Platforms that appear and disappear;
+ Falling tennis balls that must be avoided.

![screenshot](dodge-obstacles.png)

You could even create more than one backdrop, and move to the next level when your character reaches the brown door:

```blocks
    if <touching color [#714300] ?> then
        змінити тло на [наступне тло v]
        перемістити в x:(-210) y:(-120)
        чекати (1) секунд
    end
```

## Збережіть свій проект {.save}

## Виклик: Вдосконалюємо гравітацію {.challenge}

There's one other small bug in your game: gravity doesn't pull your character downwards if *any* part of it is touching a blue platform - even it's head! You can test this out by climbing most of the way up a pole and then moving to the left.

![screenshot](dodge-gravity-bug.png)

Can you fix this bug? To do this, you need to give your character different coloured trousers (on *all* costumes)...

![screenshot](dodge-trousers.png)

...and then replace the code:

```blocks
    < touching color [#0000FF]? >
```

with:

```blocks
    < color [#00FF00] is touching [#0000FF]? >
```

Remember to test your improvements to make sure you've fixed the bug!

## Збережіть свій проект {.save}

## Виклик: Більше життів {.challenge}

Can you give your player 3 `lives` {.blockdata}, instead of just sending them back to the beginning each time? Here's how your game could work:

+ Your player starts with 3 lives;
+ Whenever your player gets hit, one life is lost and they go back to the start;
+ If there are no lives left, the game ends.

## Збережіть свій проект {.save}
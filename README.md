# Bonjour, je suis 0X00 👋

![banner or gif](link_to_a_banner_or_gif)

## 🌱 Qui suis-je ?

- 🌐 Je suis un développeur Full Stack en devenir.
- 🌟 Je m'intéresse à plusieurs langages et technologies, y compris: C, C++, Java, JavaScript, Python, Bash, TypeScript, Lua, MongoDB, React, ReactJS, NodeJS, SQL, Ruby, Perl, et bien d'autres.
- 🌈 Je parle couramment le français et j'apprends l'anglais et le japonais. Mon objectif est de parler 5 langues.
- 🎓 J'ai déjà des connaissances en HTML, CSS et de bonnes bases en C.

## 🚀 Compétences

- **Langages de programmation**: `C, C++, Java, JavaScript, Python, Bash, TypeScript, Lua, Ruby, Perl`
- **Web & Front-end**: `HTML, CSS, React, ReactJS`
- **Base de données**: `MongoDB, SQL`
- **Autre**: `NodeJS`

## 📊 Statistiques GitHub

[![My_github_stat](https://github-readme-stats.vercel.app/api?username=0x00Ditto&show_icons=true&hide_border=true)]

## 🎮 Projet: Snake Game

J'ai créé un petit jeu Snake pour rendre ce README plus interactif et amusant. Profitez-en !

```python
import random
import curses

def main(stdscr):
    # Initialiser la fenêtre
    curses.curs_set(0)
    sh, sw = stdscr.getmaxyx()
    w = curses.newwin(sh, sw, 0, 0)
    w.keypad(1)
    w.timeout(100)
    
    # Initialiser la position du serpent
    snk_x = sw//4
    snk_y = sh//2
    snake = [
        [snk_y, snk_x],
        [snk_y, snk_x-1],
        [snk_y, snk_x-2]
    ]
    
    # Initialiser la nourriture
    food = [sh//2, sw//2]
    w.addch(int(food[0]), int(food[1]), curses.ACS_PI)
    
    # Initialiser la direction du serpent
    key = curses.KEY_RIGHT
    
    # Boucle du jeu
    score = 0
    while True:
        next_key = w.getch()
        key = key if next_key == -1 else next_key
        
        # Vérifier si le serpent a atteint les limites de la fenêtre ou s'est mordu lui-même
        if (
            snake[0][0] in [0, sh] or 
            snake[0][1]  in [0, sw] or 
            snake[0] in snake[1:]
        ):
            curses.endwin()
            quit()
        
        # Vérifier si le serpent a obtenu la nourriture
        new_head = [snake[0][0], snake[0][1]]
        
        if key == curses.KEY_DOWN:
            new_head[0] += 1
        if key == curses.KEY_UP:
            new_head[0] -= 1
        if key == curses.KEY_LEFT:
            new_head[1] -= 1
        if key == curses.KEY_RIGHT:
            new_head[1] += 1
        
        snake.insert(0, new_head)
        
        if (
            snake[0][0] == food[0] and
            snake[0][1] == food[1]
        ):
            score += 1
            food = None
            while food is None:
                nf = [
                    random.randint(1, sh-1),
                    random.randint(1, sw-1)
                ]
                food = nf if nf not in snake else None
            w.addch(food[0], food[1], curses.ACS_PI)
        else:
            tail = snake.pop()
            w.addch(int(tail[0]), int(tail[1]), ' ')
        
        w.addch(int(snake[0][0]), int(snake[0][1]), curses.ACS_CKBOARD)

if __name__ == "__main__":
    curses.wrapper(main)

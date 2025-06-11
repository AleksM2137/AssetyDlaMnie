        from asciimatics.effects import Print, Stars
        from asciimatics.renderers import StaticRenderer
        from asciimatics.scene import Scene
        from asciimatics.screen import Screen
        
        
        class IntroRenderer(StaticRenderer):
            def __init__(self, width):
                self.klatki = []
                szerokosc_karty = 7
        
                for i in range(width // 2 - szerokosc_karty, szerokosc_karty, -3):
        
                    lewy_x = (width // 2) - i - szerokosc_karty#obliczmy lewy x
        
                    prawy_x = (width // 2) + i #obliczmy prawy x (że prawa karta)
        
                    dziura = prawy_x - lewy_x - szerokosc_karty if prawy_x > lewy_x else 0
        
                    klatka = [#robimy klatki
                        " " * lewy_x + "┌─────┐" + " " * dziura + "┌─────┐     ",
                        " " * lewy_x + "│ ♠   │" + " " * dziura + "│ ♥   │     ",
                        " " * lewy_x + "│  K  │" + " " * dziura + "│  J  │     ",
                        " " * lewy_x + "└─────┘" + " " * dziura + "└─────┘     "
                    ]
                    self.klatki.append("\n".join(klatka))
        
                eksplozja = [# ekplozja
                    "   ╲   ╱   ",
                    " ──  *  ── ",
                    "   ╱   ╲   ",
                    " START GRY!"
                ]
        
                for _ in range(15):
                    wycentrowana_eksplozja = []# centrójemy eksplozje
                    for linja in eksplozja:
                        wycentrowana_linja = linja.center(width)
                        wycentrowana_eksplozja.append(wycentrowana_linja)
                    self.klatki.append("\n".join(wycentrowana_eksplozja))
        
                super().__init__(self.klatki)#za pomocą renderera renderujemy
        
        
        def graj_intro(screen):
            renderer = IntroRenderer(screen.width)
            effects = [
                Print(screen,
                      renderer,
                      x=0,
                      y=screen.height // 2 - 2,
                      clear=True,
                      transparent=False,
                      speed=1,
                      colour=Screen.COLOUR_WHITE),
                Stars(screen, count=100)
            ]
        
            screen.play([Scene(effects, duration=len(renderer.klatki))], repeat=False)
        
        
        if __name__ == "__main__":
            Screen.wrapper(graj_intro)
i
        
        from asciimatics.effects import Print
        from asciimatics.renderers import StaticRenderer
        from asciimatics.scene import Scene
        from asciimatics.screen import Screen
        
        class BGRenderer(StaticRenderer):
            def __init__(self):
                
        
                bg = [
                    '                                                                                   O     ',
                    '                                                                                  /|     ',
                    '                                                                                 / |     ',
                    '                                                                                /__|     ',
                    '                                                                                   |     ',
                    '                                                                                   |     ',
                    '                                                                                   |     ',
                    '                                                                                   |     ',
                    '                                                            ___________            |     ',
                    '                                                           |           |           |     ',
                    '                                                            ‾‾‾‾‾‾‾‾‾‾‾            |     ',
                    '                                                                                   |     ',
                    '                                            ___________                            |     ',
                    '                                           |           |                           |     ',
                    '                                            ‾‾‾‾‾‾‾‾‾‾‾                            |     ',
                    '                                                                                   |     ',
                    '                    ___________                                                    |     ',
                    '                   |           |                                                   |     ',
                    '                    ‾‾‾‾‾‾‾‾‾‾‾                                                 |‾‾‾‾‾|  ',
                    '                                                                                |     |  ',
                    '‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾'
                ]
        
        
                super().__init__(["\n".join(bg)])
        class IntroRenderer(StaticRenderer):
            def __init__(self, width):
                self.klatki = []
                wysokość_ludzika = 9
                ludzik = [
                    '/‾‾‾\\',
                    '| O O|',
                    '\\___/',
                    '  |   ',
                    ' /|\\ ',
                    '/ | \\',
                    '  |   ',
                    ' / \\ ',
                    '/   \\'
                ]
                # pozycje = [
                #     (0, 11), (5, 11), (10, 11), (15, 11), (40, 10), (50, 12), (60, 14), (70, 10),
                #     (60, 8), (50, 6), (40, 4), (30, 2), (20, 1)
                # ]
                pozycje_y = [11,11,11,11,8,8,8,8,4,4,4,4,0,0,0,0,1,2,3,4,5,6,7,8,9,10,11]
                pozycje = [
                    (i,pozycje_y[i//5]) for i in range(0,80,5) for _ in range(2) 
                ]
                pozycje.extend((75,poz_y) for poz_y in pozycje_y[16:])
                for poz in pozycje:
                    klatka = [' ' * width for _ in range(20)]
                    x, y = poz
                    for i, linia in enumerate(ludzik):
                        if 0 <= y + i < 20:
                            # Wstaw ludzika w odpowiednie miejsce
                            linia_klatki = list(klatka[y + i])
                            linia_klatki[x:x+len(linia)] = linia
                            klatka[y + i] = ''.join(linia_klatki)
                    self.klatki.append('\n'.join(klatka))
        
                eksplozja = [# ekplozja
                    "   ╲   ╱   ",
                    " ──  *  ── ",
                    "   ╱   ╲   ",
                    " START GRY!"
                ]
        
                for _ in range(15):
                    wycentrowana_eksplozja = []# centrójemy eksplozje
                    for linja in eksplozja:
                        wycentrowana_linja = linja.center(width)
                        wycentrowana_eksplozja.append(wycentrowana_linja)
                    self.klatki.append("\n".join(wycentrowana_eksplozja))
        
                super().__init__(self.klatki)#za pomocą renderera renderujemy
        
        
        def graj_intro(screen):
            renderer = IntroRenderer(screen.width)
            renderer2 = BGRenderer()
            effects = [
                Print(screen,
                    renderer2,
                    x=0,
                    y=screen.height // 2 - 2,
                    clear=True,           # Tło czyści ekran
                    transparent=False,
                    speed=1,
                    colour=Screen.COLOUR_WHITE),
                Print(screen,
                    renderer,
                    x=0,
                    y=screen.height // 2 - 2,
                    clear=False,          # Animacja NIE czyści ekranu
                    transparent=True,
                    speed=1,
                    colour=Screen.COLOUR_WHITE)
            ]
        
            screen.play([Scene(effects, duration=len(renderer.klatki))], repeat=False)
        
        
        if __name__ == "__main__":
            Screen.wrapper(graj_intro)

i

                from asciimatics.effects import Print
                from asciimatics.renderers import StaticRenderer
                from asciimatics.scene import Scene
                from asciimatics.screen import Screen
                
                
                class IntroRenderer(StaticRenderer):
                    def __init__(self, height,width):
                        self.klatki = []
                        klatka = []
                        klatka.extend([""] * (height-8))
                        klatka.append("‾"*width)
                        self.klatki.append("\n".join(klatka))
                
                        for i in range(height-15):
                            klatka = []
                            klatka.extend([""] * (i))  # Dodajemy puste linie na górze, im większe i, tym niżej ludzik
                            klatka.extend([
                                " "*(width//2)+"           ",
                                " "*(width//2)+"  /‾‾‾‾‾‾\\ ",
                                " "*(width//2)+"  | O  O | ",
                                " "*(width//2)+"  | ---- | ",
                                " "*(width//2)+"  \\______/ ",
                                " "*(width//2)+"  _|_||_|_ ",
                                " "*(width//2)+" | |_||_| |",
                                " "*(width//2)+"  ‾| || |‾ ",
                                " "*(width//2)+"    ‾  ‾    "
                            ])
                            self.klatki.append("\n".join(klatka))
                
                        klatka = []
                        klatka.extend([""] * (height-8))
                        klatka.append("‾"*(width//2+1)+"‾\\______/‾"+"‾"*(width//2))
                        self.klatki.append("\n".join(klatka))
                        eksplozja = [# ekplozja
                            "   ╲   /   ",
                            " ──  *  ── ",
                            "   /   ╲   ",
                            " START GRY!"
                        ]
                
                        for _ in range(15):
                            wycentrowana_eksplozja = []# centrójemy eksplozje
                            for linja in eksplozja:
                                wycentrowana_linja = linja.center(width)
                                wycentrowana_eksplozja.append(wycentrowana_linja)
                            self.klatki.append("\n".join(wycentrowana_eksplozja))
                
                        super().__init__(self.klatki)#za pomocą renderera renderujemy
                
                
                def graj_intro(screen):
                    renderer = IntroRenderer(screen.height,screen.width)
                    effects = [
                        Print(screen,
                                renderer,
                                x=0,
                                y=0,
                                clear=True,
                                transparent=False,
                                speed=1,
                                colour=Screen.COLOUR_WHITE)
                    ]
                
                    screen.play([Scene(effects, duration=len(renderer.klatki))], repeat=False)
                
                
                if __name__ == "__main__":
                    Screen.wrapper(graj_intro)

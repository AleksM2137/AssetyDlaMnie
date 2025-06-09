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
        

import pygame
import sys
import random
from pygame import mixer

mixer.init()
pygame.init()
screen_width,screen_height = 600,600
screen = pygame.display.set_mode((screen_width, screen_height))

clock = pygame.time.Clock()

WHITE = (255, 255, 255)
BLACK = (0,0,0)
RED = (255,0,0)
GREEN = (0,255,0)
BLUE = (0,0,255)
TEXT_COLOR = (4,170,10)

done_moving = 0
def Win():
    global done_moving
    if done_moving >= 4:
        if Image_1.print_image_name == Image_2.print_image_name and Image_1.print_image_name == Image_3.print_image_name and Image_1.print_image_name == Image_4.print_image_name:
            show_text.display_text = 'SUPPER WIN!!!!'
            mixer.music.load(r"528958__beetlemuse__level-up-mission-complete.wav")
        elif Image_2.print_image_name == Image_3.print_image_name and Image_2.print_image_name == Image_4.print_image_name:
            show_text.display_text = 'WIN!!!!'
            mixer.music.load(r"522246__dzedenz__result-7.mp3")
        else:
            show_text.display_text = 'YOU LOST'
            mixer.music.load(r"162465__kastenfrosch__lostitem.mp3")
        show_text.update_text()
        mixer.music.play()
        done_moving = 0

class Show_Text():
    def __init__(self):
        self.display_text = 'Play'
        self.font = pygame.font.Font('freesansbold.ttf', 32)
        self.text = self.font.render(self.display_text, True, BLACK)
        self.textRect = self.text.get_rect()
        self.textRect.center = (300,50)

    def update_text(self):
        self.display_text = self.display_text
        self.text = self.font.render(self.display_text, True, BLACK)
        self.textRect = self.text.get_rect()
        self.textRect.center = (300,50)

    def update(self):
        self.update_text()
        screen.blit(self.text,self.textRect)

class Show_Image():
    def __init__(self,x,y):
        self.position = (x,y)
        self.image_list = [r"pineapple.png",
                           r"watermelon.png",
                           r"mango.png",
                           r"lemon.png",
                           r"grapes.png",
                           r"orange-juice.png",
                           r"apple.png"]
        
        self.animation_timer = 0
        self.end_animation = 10
        self.current_image = 0
        self.image = pygame.image.load(random.choice(self.image_list))
        self.transform_image = pygame.transform.scale(self.image,(100,100))
        self.image_rect = pygame.Rect(self.position,(100,100))
        self.turning = False
        self.print_image_name = self.image_list[int(self.current_image)]

    def animate(self):
        mixer.music.load(r"241848__sengjinn__jewelry-ring-spin-01 (1).wav")
        mixer.music.play()
        self.turning = True
        show_text.display_text = 'SPINNING'
        show_text.update_text()

    def update(self):
        global done_moving
        if self.turning == True:
            self.animation_timer += 0.1
            self.current_image = random.randint(0,6)

            if int(self.animation_timer) >= self.end_animation:
                self.animation_timer = 0
                lever.animate_lever()
                self.turning = False
                done_moving += 1

        self.image = pygame.image.load(self.image_list[int(self.current_image)])
        self.transform_image = pygame.transform.scale(self.image,(100,100))
        self.print_image_name = self.image_list[int(self.current_image)]
        screen.blit(self.transform_image,self.image_rect)

class Lever(object):
    def __init__(self,x,y):
        self.position = (x,y)
        self.image = pygame.image.load(r"pngtree-lever-of-inclusion-icon-cartoon-style-png-image_1895232.jpg").convert()
        self.transform_image = pygame.transform.scale(self.image,(100,100))
        self.angle = -90
        self.rotate_image = pygame.transform.rotate(self.transform_image, self.angle)
        self.image_rect = pygame.Rect(self.position,(100,100))
        self.clickable = True

    def animate_lever(self):
        self.clickable = True

    def on_click(self,event):
        if event.type == pygame.MOUSEBUTTONDOWN and self.clickable == True:
            if event.button == 1:
                if self.image_rect.collidepoint(event.pos):
                    self.clickable = False
                    Image_1.animate()
                    Image_2.animate()
                    Image_3.animate()
                    Image_4.animate()

        if self.clickable == True:
            self.angle = -90
        else:
            self.angle = 90
        self.rotate_image = pygame.transform.rotate(self.transform_image, self.angle)
        self.image_rect = pygame.Rect(self.position,(100,100))
                    
    def update(self):
        screen.blit(self.rotate_image,self.image_rect)
        
show_text = Show_Text()
lever = Lever(500,200)
Image_1 = Show_Image(100,200)
Image_2 = Show_Image(200,200)
Image_3 = Show_Image(300,200)
Image_4 = Show_Image(400,200)
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
        lever.on_click(event)

    screen.fill(WHITE)

    show_text.update()

    lever.update()
    Image_1.update()
    Image_2.update()
    Image_3.update()
    Image_4.update()
    Win()

    clock.tick(60)
    pygame.display.flip()
    pygame.display.update()

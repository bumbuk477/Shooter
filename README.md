# Shooter
#Створи власний Шутер!

import pygame
import pygame.display
import pygame.mixer_music
win_width = 700
win_heigth = 500
window = pygame.display.set_mode((win_width,win_heigth))
pygame.display.set_caption("Shoter")
FPS = pygame.time.Clock()
game = True
finish = False

pygame.mixer.init()
pygame.mixer.music.load("space.ogg")
pygame.mixer.music.play(-1)
pygame.mixer.music.set_volume(0.4)

class Settings():
    def __init__(self,image,x,y,w,h):
        self.image = pygame.image.load(image)
        self.image = pygame.transform.scale(self.image,(w,h))
        self.rect=self.image.get_rect()
        self.x = x
        self.y = y
    
    def draw(self):
        window.blit(self.image,(self.rect.x,self.rect.y))


class Player(Settings):
    def __init__(self,image,x,y,w,h,s,hp):
        super().__init__(image,x,y,w,h)
        self.speed = s
        self.hp = hp
        self.image_heart = pygame.image.load("HP.png")
        self.image_heart = pygame.transform.scale(self.image_heart,(50,50))

    def move(self):
        keys = pygame.key.get_pressed()
        if keys [pygame.K_a] and self.rect.x>0:
            self.rect.x -= self.speed
        if keys[pygame.K_w]and self.rect.y>0:
            self.rect.y -= self.speed
        if keys[pygame.K_s]and self.rect.y<win_heigth-self.rect.height:
            self.rect.y += self.speed
        if keys[pygame.K_d]and self.rect.x< win_width - self.rect.width:
            self.rect.x += self.speed
    def show_hearts(self):
        for h in range(self.hp):
            window.blit(self.image_heart,(win_width-50-h*50,0))



fon  = Settings("galaxy.jpg",0,0,win_width,win_heigth)
player = Player("rocket.png",win_width//2,win_heigth-100,100,100,10,3)

while game:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game =False
    if finish != True:
        fon.draw()
        player.draw()
        player.move()
        
    pygame.display.flip()
    FPS.tick(60)

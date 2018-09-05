# mycode
first
##import name_module
##name_module.name()
##from cf_module import *
##c=float(input('enter a number'))
##f=ctof(c)
##print(f)
##import cf_module
##c=float(input('enter a number'))
##f=cf_module.ctof(c)
##print(f)
import time,random
##L=[]
##for i in range(5):
## L.append(random.randint(1,20))
##print(L)
for i in range(10):
    print(random.random())
    time.sleep(3)
 18   
import pygame,sys
from pygame.locals import *
pygame.init()
class Ballclass(pygame.sprite.Sprite):
    def __init__(self,image_file,location,speed):
        pygame.sprite.Sprite.__init__(self)
        self.image=pygame.image.load(image_file)
        self.rect=self.image.get_rect()
        self.rect.left,self.rect.top=location
        self.speed=speed
    def move(self):
        global points , score_text
        self.rect=self.rect.move(self.speed)
        if self.rect.left<0 or self.rect.right>screen.get_width():
            self.speed[0]=-self.speed[0]
        if self.rect.top<0:
            self.speed[1]=-self.speed[1]
            points=points+1
            score_text=font.render(str(points),True,[0,0,0])
class Paddleclass(pygame.sprite.Sprite):
    def __init__(self,location=[0,0]):
        pygame.sprite.Sprite.__init__(self)
        image_surface=pygame.surface.Surface([100,20])
        image_surface.fill([0,0,0])
        self.image=image_surface.convert()#使用图形转化为图形文件
        self.rect=self.image.get_rect()
        self.rect.left,self.rect.top=location
screen=pygame.display.set_mode([600,480])
clock=pygame.time.Clock()
myball=Ballclass(r'C:\Program Files\Python37\Lib\site-packages\images\wackyball.bmp',[50,50],[10,5])
ballGroup=pygame.sprite.Group(myball)
mypaddle=Paddleclass([250,440])
lives=3
points=0

font=pygame.font.Font(None,50)
score_text=font.render(str(points),True,[0,0,0])
textpos=[10,10]
done=False

while True:
    clock.tick(30)
    screen.fill([255,255,255])
    for event in pygame.event.get():
        if event.type==pygame.QUIT:
            pygame.quit()
            sys.exit()
        elif event.type==pygame.MOUSEMOTION:
            mypaddle.rect.centerx=event.pos[0]
    if pygame.sprite.spritecollide(mypaddle,ballGroup,False):
         myball.speed[1]=-myball.speed[1]
    myball.move()

    if not done:   
      screen.blit(myball.image,myball.rect)
      screen.blit(mypaddle.image,mypaddle.rect)#重绘
      screen.blit(score_text,textpos)
      for i in range(lives):
         width=screen.get_width()
         screen.blit(myball.image,[(width-40*i),20])
      pygame.display.flip()

    if myball.rect.top>=screen.get_rect().bottom:
        lives=lives-1
        if lives==0:
            final_text1='GAME OVER'
            final_text2='Your final score is:'+str(points)
            ft1_font=pygame.font.Font(None,70)
            ft1_surf=font.render(final_text1,1,[0,0,0])
            ft2_font=pygame.font.Font(None,50)
            ft2_surf=font.render(final_text2,1,[0,0,0])
            screen.blit(ft1_surf,[int(screen.get_width()/2-ft1_surf.get_width()/2),100])
            screen.blit(ft2_surf,[int(screen.get_width()/2-ft2_surf.get_width()/2),200])
            pygame.display.flip()
            done=True
        else:
            pygame.time.delay(2000)
            myball.rect.topleft=[50,50]

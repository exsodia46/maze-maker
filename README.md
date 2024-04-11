import pygame 
from player import player
pygame.init()
pygame.display.set_caption("top down grid game")
screen = pygame.display.set_mode((1000, 800))
clock = pygame.time.Clock()
gameover = False


p1 = player()

#constants
LEFT = 0
RIGHT = 1
UP = 2
DOWN = 3
SPACE = 4
w = 5
keys = [False,False,False,False, False]


map = [[2,3,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2],
       [2,0,0,0,0,2,2,4,0,2,0,0,0,0,3,0,2,2,2,2],
       [2,0,0,0,4,2,2,1,1,2,0,2,2,2,2,0,0,0,0,2],
       [2,0,0,2,2,2,2,0,0,2,0,2,4,0,1,0,2,2,0,2],
       [2,2,0,0,0,0,0,0,0,2,0,2,2,0,1,0,0,0,0,2],
       [2,0,0,0,1,0,0,0,0,2,0,2,0,1,2,0,2,2,2,2],
       [2,0,2,0,0,2,2,0,0,2,0,2,0,0,2,0,0,0,0,2],
       [2,0,2,0,0,2,2,0,0,2,0,2,0,0,2,2,2,2,0,2],
       [2,0,0,0,0,0,0,0,0,3,0,2,1,0,2,2,2,0,0,2],
       [2,2,2,3,2,2,2,2,2,2,2,2,0,0,0,0,0,0,3,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,2,2,2,2,2,0,2],
       [2,3,2,2,2,2,0,2,2,2,2,2,2,2,2,2,2,2,0,2],
       [2,0,2,4,2,0,0,2,2,4,0,1,1,1,0,0,0,2,0,2],
       [2,0,2,1,0,2,2,2,2,2,2,2,2,2,2,2,3,2,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,0,3],
       [2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2]]

brick = pygame.image.load('brick.png')
dirt = pygame.image.load('dirt.png')
door = pygame.image.load('door.png')
chest = pygame.image.load('chest.png')

while not gameover:
    clock.tick(60)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            gameover = True
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                keys[LEFT] = True
            elif event.key == pygame.K_RIGHT:
                keys[RIGHT] = True

        elif event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT:
                keys[LEFT] = False
            elif event.key == pygame.K_RIGHT:
                keys[RIGHT] = False
        
 #physics-----------------------------------------------------------------------------------------
p1.move(keys, map)


 #renders-----------------------------------------------------------------------------------------
p1.draw(screen)


screen.fill((0,0,0))

for i in range(16):
        for j in range(20):
            if map[i][j] == 1:
                screen.blit(dirt, (j * 50, i * 50), (0, 0, 50, 50))
            if map[i][j] == 2:
                screen.blit(brick, (j * 50, i * 50), (0, 0, 50, 50))
            if map[i][j] == 3:
                screen.blit(door, (j * 50, i * 50), (0, 0, 50, 50))
            if map[i][j] == 4:
                screen.blit(chest, (j * 50, i * 50), (0, 0, 50, 50))
pygame.display.flip()



pygame.quit()

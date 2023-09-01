# drop_pico8

```lua

basket_sprite = 8
player_sprite = 1

player_x = 64
player_y = 100

fruits = {}
fruit_start = 2
fruit_count = 6
fruit_interval = 24

gravity = 0.8
level = 1
points = 0

function _init()
    for i=1,level do
        fruit={
            sprite=flr(rnd(fruit_count)+fruit_start),
            x=flr(rnd(100)+5),
            y=i*(-fruit_interval)
        }
        add(fruits,fruit)
    end
end

function _update60()
    if btn(0) then player_x-=2.0 end
    if btn(1) then player_x+=2.0 end

    for fruit in all(fruits) do
        fruit.y+=gravity

        if  fruit.y+5>=player_y-8
        and fruit.y+5<=player_y
        and fruit.x+5>=player_x
        and fruit.x<=player_x+8 then
            points+=1
            del(fruits,fruit)
        end

        if fruit.y>100 then
            del(fruits,fruit)
        end
    end

    if #fruits==0 then
        level+=1
        _init()
    end
end

function _draw()
    cls()
    rectfill(0,108,127,127,5)
    spr(player_sprite,player_x,player_y)
    spr(basket_sprite,player_x,player_y-8)

    for fruit in all(fruits) do
        spr(fruit.sprite,fruit.x,fruit.y)
    end

    print("score= "..points, 7)
end

```

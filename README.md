# SistemaSolar
Implementei um conceito que já havia sido criado, distancia entre o sol e a terra(uma unidade astronômica), subtraí, multipliquei e potencializei essa distancia para definir a posição dos planetas em relação ao sol utilizando o pacote gráfico vPython.


from vpython import *

scene.width=1260
scene.height=630


#Tamanho dos planetas
solRadius = 0.7
mercurioRadius = solRadius * 0.29 #raio de 2k km
venusRadius = solRadius * 0.35 #raio de 6k km
terraRadius = solRadius * 0.4 #raio de 6.3k km
luaRadius = terraRadius * 0.27
marteRadius = solRadius * 0.3 #raio de 3k km
jupiterRadius = solRadius * 0.57 #raio de 69k km
saturnoRadius = solRadius * 0.48 #raio de 58k km
saturnoRingRadius = saturnoRadius + 0.17
uranoRadius = solRadius * 0.42 #raio de 25k km
netunoRadius = solRadius * 0.38 #raio de 24k km

#Unidade astronomica
astronomicalUnit = 4.0

mercurioAngle = 0
venusAngle = 0
earthAngle = 0
moonAngle = 0
marsAngle = 0
jupiterAngle = 0
saturnoAngle, saturnoRingAngle = 0, 0
uranoAngle = 0
netunoAngle= 0

#distancia entre terra e Lua
earthMoonDistance = terraRadius * 2

#Rotação dos planetas
mercurioOrbitRate = 1
venusOrbitRate = 1
earthOrbitRate = 1
moonOrbitRate = 13
marsOrbitRate = 1
jupiterOrbitRate = 1
saturnoOrbitRate = 1
saturnoRingOrbitRate = 1
uranoOrbitRate = 1
netunoOrbitRate = 1

#Sol
sol = sphere(radius=solRadius, opacity=0.9, emissive=True, color=color.yellow)
sunlight = local_light(pos=vec(0,0,0), color=color.white)
more_sunlight=local_light(pos=vec(0,0,0), color=color.white)

#Planeta Mercurio
mercurio = sphere(radius=mercurioRadius,
               texture=textures.gravel,
               flipx=False,
               shininess=0.9,
               make_trail=True)

#Planeta Venus
venus = sphere(radius=venusRadius,
               texture=textures.stucco,
               color=color.orange,
               flipx=False,
               shininess=0.9,
               make_trail=True)

#Planeta Terra
terra = sphere(radius=terraRadius,
               texture=textures.earth,
               flipx=False,
               shininess=0.9,
               make_trail=True)

#Lua
lua = sphere(radius=luaRadius,
             color=color.gray(0.2),
             flipx=True,
             flipy=True,
             shininess=0.9)

#Planeta Marte
marte = sphere(radius=marteRadius,
               color=color.red,
               texture=textures.wood,
               flipx=False,
               shininess=0.9,
               make_trail=True)

#Planeta Jupiter
jupiter = sphere(radius=jupiterRadius,
                 texture=textures.wood_old,
                 flipx=False,
                 shininess=0.9,
                 make_trail=True)

#Planeta Saturno
saturno = sphere(radius=saturnoRadius,
                 texture=textures.wood,
                 flipx=False,
                 shininess=0.8,
                 make_trail=True)

#Anel de Saturno
anelSaturno = ring(radius=saturnoRingRadius,
                   thickness=0.03,
                   texture=textures.wood,
                   axis=vec(0, 3, 0))

#Planete Urano
urano = sphere(radius=uranoRadius,
               texture=textures.wood,
               color=color.cyan,
               shininess=0.7,
               make_trail=True
               )

#Planeta Netuno
netuno = sphere(radius=netunoRadius,
                color=color.blue,
                shininess=0.7,
                make_trail=True)

#Foco da camera
scene.camera.follow(terra)

#Velocidades orbitais e rotacionais
netunoSpeed = 0.001
uranoSpeed = 0.002
saturnoSpeed = 0.005
jupiterSpeed = 0.009
marsSpeed = 0.017
earthSpeed = 0.02
venusSpeed = 0.025
mercurioSpeed = 0.05
SunRotate = 0.01

#Inicio do ciclo do sistema solar
while True:
    rate(100)

    #Posição dos planetas em relação ao sol
    terra.pos = vec(astronomicalUnit * cos(radians(earthAngle)), 0, astronomicalUnit * sin(radians(earthAngle)))
    lua.pos = terra.pos + vec(earthMoonDistance * cos(radians(moonAngle)), 0, earthMoonDistance * sin(radians(moonAngle)))
    marte.pos = vec((astronomicalUnit * 2) * cos(radians(marsAngle)), 0, (astronomicalUnit * 2) * sin(radians(marsAngle)))
    mercurio.pos = vec((astronomicalUnit-3)*cos(radians(mercurioAngle)), 0, (astronomicalUnit-3)*sin(radians(mercurioAngle)))
    venus.pos = vec((astronomicalUnit-1.4)*cos(radians(venusAngle)), 0, (astronomicalUnit-1.5)*sin(radians(venusAngle)))
    jupiter.pos = vec((astronomicalUnit**2)*cos(radians(jupiterAngle)), 0, (astronomicalUnit**2)*sin(radians(jupiterAngle)))
    saturno.pos = vec((astronomicalUnit**2.2)*cos(radians(saturnoAngle)), 0, (astronomicalUnit**2.2)*sin(radians(saturnoAngle)))
    anelSaturno.pos = vec((astronomicalUnit**2.2)*cos(radians(saturnoRingAngle)), 0, (astronomicalUnit**2.2)*sin(radians(saturnoRingAngle)))
    urano.pos = vec((astronomicalUnit**2.5)*cos(radians(uranoAngle)), 0, (astronomicalUnit**2.5)*sin(radians(uranoAngle)))
    netuno.pos = vec((astronomicalUnit**2.8)*cos(radians(netunoAngle)), 0, (astronomicalUnit**2.8)*sin(radians(netunoAngle)))

    #Orbita em volta do sol
    mercurioAngle -= mercurioOrbitRate * mercurioSpeed
    venusAngle -= venusOrbitRate * venusSpeed
    earthAngle -= earthOrbitRate * earthSpeed
    moonAngle -= moonOrbitRate * earthSpeed
    marsAngle -= marsOrbitRate * marsSpeed
    jupiterAngle -= jupiterOrbitRate * jupiterSpeed
    saturnoAngle -= saturnoOrbitRate * saturnoSpeed
    saturnoRingAngle -= saturnoRingOrbitRate * saturnoSpeed
    uranoAngle -= uranoOrbitRate * uranoSpeed
    netunoAngle -= netunoOrbitRate * netunoSpeed


    #Rotação das sphere(planetas)
    mercurio.rotate(angle=radians(mercurioSpeed*360), axis=vec(0, 1, 0))
    venus.rotate(angle=radians(venusSpeed*360), axis=vec(0, 1, 0))
    terra.rotate(angle=radians(earthSpeed * 360), axis=vec(0, 1, 0))
    lua.rotate(angle=radians(earthSpeed * moonOrbitRate), axis=vec(0, 1, 0))
    sol.rotate(angle=radians(SunRotate * 16), axis=vec(0, 1, 0))
    marte.rotate(angle=radians(marsSpeed * 360), axis=vec(0, 1, 0))
    jupiter.rotate(angle=radians(jupiterSpeed*360), axis=vec(0, 1, 0))
    saturno.rotate(angle=radians(saturnoSpeed*360), axis=vec(0, 1, 0))
    anelSaturno.rotate(angle=radians(saturnoSpeed*360), axis=vec(0, 1, 0))
    urano.rotate(angle=radians(uranoSpeed*360), axis=vec(0, 1, 0))
    netuno.rotate(angle=radians(netunoSpeed*360), axis=vec(0, 1, 0))

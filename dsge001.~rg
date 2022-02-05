setwd "C:\Users\Usuario\Dropbox\Coding\Eviews\"

setmaxerrs 3
wfclose
wfcreate(wf=dsge001) m 2000 2022
rndseed 1
series t = @trend
scalar nn= @obssmpl
scalar mm = nn-1
smpl @all if t=0

scalar A = 100
scalar alfa = 0.5
scalar pmc = 0.8
scalar delta = 0.03
scalar s= 1-pmc


series k = 100
series y = A*k^alfa
series cons = pmc*y
series i = y - cons

smpl @all

for !i=1 to mm
!j = !i+1
smpl @all if t=!i
series k = A*k(-1)^alfa+(1-delta)*k(-1)-cons(-1)
series y = A*k^alfa
series i = k - (1-delta)*k(-1)
series cons = y - i
next

smpl @all

series u = log(cons)
series umgc = 1/cons
series crec = log(y)
series dk = delta*k
series sy = s*y

group grupo1 y k cons i u umgc crec
freeze(mode=overwrite, grafico1) grupo1.line(m)
show grafico1

group grupo2 k dk sy y
freeze(mode=overwrite, grafico2) grupo2.scat
show grafico2


'graf2b.axis overlap
'graf2b.setelem(2) axis(r)

wfsave dsge001.wf1


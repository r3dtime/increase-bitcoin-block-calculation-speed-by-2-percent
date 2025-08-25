# increase bitcoin block calculation speed by 2 percent
Hi! I want to share with you a solution that will save time on hash generation, which ultimately leads to energy savings.
I'll take Bitcoin block generation as an example.
```
def row(a:int, b:int, c:int, d:int, e:int, f:int, g:int, h:int, k:int, dt:int):
    t1 = (h + si1(e) + _ch(e, f, g) + k + dt) & 0xffffffff
    t2 = (si0(a) + _maj(a, b, c)) & 0xffffffff
    h = g
    g = f
    f = e
    e = (d + t1) & 0xffffffff
    d = c
    c = b
    b = a
    a = (t1 + t2) & 0xffffffff
    return a,b,c,d,e,f,g,h

data = 0
a,b,c,d,e,f,g,h = row(a, b, c, d, e, f, g, h, keys[0], data)
```
We got these numbers (a: 4228417613, e: 2563236514) from the first iteration of the first block by setting the value 0 for the date variable.
Now we can use these numbers as constants without having to recalculate.
By doing this we reduced the calculation time by 1%. To bring it to 2% we can use the pre-calculated cache (sec) for the second iteration.
```
def ae2(dt0, dt1, sec, starts):
    a1 = (dt0 + 4228417613) & 0xffffffff
    e1 = (dt0 + 2563236514) & 0xffffffff
    a0 = (dt1 + (sec[dt0] >> 32)) & 0xffffffff
    e0 = (dt1 + (sec[dt0] & 0xffffffff)) & 0xffffffff
    return a0, a1, starts[0], starts[1], e0, e1, starts[4], starts[5]
```

Your financial support will help me continue to work on optimizing the code and finding new solutions to speed up the Bitcoin mining process.

<p>
  <img src="btc.jpeg" width="150" title="btc">
  <p>BTC: 1EKcUWSVZ8Hua88x9sqp24bbyR6Ttw6DJJ</p>
</p>


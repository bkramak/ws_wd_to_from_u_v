# ws_wd_to_from_u_v

Working with wind speed and direction using their u and v vector representations isn't hard, once you understand WHY certain steps have to be done.

for those short on patience or time, please consider these functions:

```python

def uv_from_wswd2(ws, wd):
    # source = http://colaweb.gmu.edu/dev/clim301/lectures/wind/wind-uv
    # source 2 https://github.com/bkramak/ws_wd_to_from_u_v 
    # ws in m/s and wd in decimal degrees
    wd = 270-wd # convert from meteorlogical to math coords see website
    wd = np.where(wd < 0, wd + 360, wd) # convert from meteorlogical to math coords see website part 2
    v = ws * np.sin(np.radians(wd))
    u = ws * np.cos(np.radians(wd))
    return u, v

def wswd_from_uv2(u,v):
    # source =  http://colaweb.gmu.edu/dev/clim301/lectures/wind/wind-uv
    # source 2 https://github.com/bkramak/ws_wd_to_from_u_v 
    ws = np.round((u**2+v**2)**(1/2),3)
    wd = np.round(270-(360+np.degrees(np.arctan2(v, u)))%360,3) # 270- undoes conversion to math coords
    wd = np.where(wd < 0, wd + 360, wd) # undo part 2
    return ws, wd

```


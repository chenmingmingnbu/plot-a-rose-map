tri2=data2['tri']/data2['total']
ga2=data2['ga']/data2['total']
gb2=data2['gb']/data2['total']
het2=data2['het']/data2['total']
gamma2=data2['gamma']/data2['total']
alpha2=data2['alpha']/data2['total']
trixy=zip(tri2/2.,(tri2/2.)*3**.5)
hetxy=zip(het2,[0]*114)
gaxy=zip(ga2/2.,-(ga2/2.)*3**.5)
gbxy=zip(-gb2/2.,-(gb2/2.)*3**.5)
gammaxy=zip(-gamma2,[0]*114)
alphaxy=zip(-alpha2/2.,(alpha2/2.)*3**.5)
sinbnf=data2['sinBNF']
minsinbnf=min(sinbnf)
maxsinbnf=max(sinbnf)
fig=plt.figure()
ax=fig.add_subplot(111)
for i in range(114):
    if not math.isnan(data2['total'][i]) and not math.isnan(data2['sinBNF'][i]):
        verts=[trixy[i],hetxy[i],gaxy[i],gbxy[i],gammaxy[i],alphaxy[i],trixy[i]]
        codes=[Path.MOVETO,Path.LINETO,Path.LINETO,Path.LINETO,Path.LINETO,Path.LINETO,Path.CLOSEPOLY]
        path=Path(verts,codes)
        patch=patches.PathPatch(path,ec=(((sinbnf[i]-minsinbnf)/(maxsinbnf-minsinbnf))**.3,0,(1.-(sinbnf[i]-minsinbnf)/(maxsinbnf-minsinbnf))**.3),fc='none',lw=1.2)
        ax.add_patch(patch)
verts2=[(.5,3**.5/2.),(1,0),(.5,-3**.5/2.),(-.5,-3**.5/2.),(-1,0),(-.5,3**.5/2.),(.5,3**.5/2.)]
codes2=[Path.MOVETO,Path.LINETO,Path.LINETO,Path.LINETO,Path.LINETO,Path.LINETO,Path.CLOSEPOLY]
path2=Path(verts2,codes2)
patch2=patches.PathPatch(path2,ec='black',fc='none',lw=2)
ax.add_patch(patch2)
ax.add_line(Line2D((-.5,.5),(-3**.5/2.,3**.5/2.),color='black',linestyle='--'))
ax.add_line(Line2D((-1,1),(0,0),color='black',linestyle='--'))
ax.add_line(Line2D((-.5,.5),(3**.5/2.,-3**.5/2.),color='black',linestyle='--'))
plt.xlim(-1,1)
plt.ylim(-3**.5/2.-.1,3**.5/2.+.1)
ax.set_aspect(1)
plt.axis('off')
plt.savefig(u'各类群所占比例与单细胞固氮率的关系.pdf')# plot-a-rose-map
plot a rose map with python

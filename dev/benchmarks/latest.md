## Minecraft load time benchmark


---

<p align="center" style="font-size:160%;">
MC total load time:<br>
275.71 sec
<br>
<sup><sub>(
4:35 min
)</sub></sup>
</p>

<br>


<p align="center">
<img src="https://quickchart.io/chart?w=400&h=30&c={
  type: 'horizontalBar',
  data: {
    datasets: [
      {label:      'MODS:', data: [115.15]},
      {label: 'FML stuff:', data: [160.55]}
    ]
  },
  options: {
    scales: {
      xAxes: [{display: false,stacked: true}],
      yAxes: [{display: false,stacked: true}],
    },
    elements: {rectangle: {borderWidth: 2}},
    legend: {display: false,},
    plugins: {datalabels: {color: 'white',formatter: (value, context) =>
      [context.dataset.label, value].join(' ')
    }}
  }
}"/>
</p>

<br>

# Mods Loading Time
<p align="center">
<img src="https://quickchart.io/chart?w=400&h=300&c={
  type: 'outlabeledPie',
  options: {
    cutoutPercentage: 25,
    plugins: {
      legend: !1,
      outlabels: {
        stretch: 5,
        padding: 1,
        text: (v,i)=>[
          v.labels[v.dataIndex],' ',
          (v.percent*1000|0)/10,
          String.fromCharCode(37)].join('')
      }
    }
  },
  data: {...
`
813e81   5.75s OpenComputers;
8f304e   5.17s Astral Sorcery;
a651a8   4.72s IndustrialCraft 2;
516fa8   4.32s Ender IO;
cd922c   3.24s NuclearCraft;
5161a8   2.74s CraftTweaker2;
495797   7.06s CraftTweaker2 (Script Loading);
213664   2.53s Forestry;
308f7e   2.49s Quark: RotN Edition;
436e17   2.45s Integrated Dynamics;
ba3eb8   2.09s Cyclic;
a86e51   1.99s Extra Utilities 2;
3e8160   1.98s The Twilight Forest;
8f4d30   1.80s Open Terrain Generator;
8c2ccd   1.75s Immersive Engineering;
3eb2ba   1.65s Botania;
649e21   1.61s OpenBlocks;
814a3e   1.60s RFTools;
3e68ba   1.53s AE2 Unofficial Extended Life;
61176e   1.50s Ice and Fire;
813e80   1.48s Shadowfacts' Forgelin (Dummy);
444444  14.46s 12 Other mods;
333333  39.40s 135 'Fast' mods (load 1.0s - 0.1s);
222222   8.91s 303 'Instant' mods (load %3C 0.1s)
`
    .split(';').reduce((a, l) => {
      l.match(/(\w{6}) *(\d*\.\d*)s (.*)/)
      .slice(1).map((a, i) => [[String.fromCharCode(35),a].join(''), parseFloat(a), a][i])
      .forEach((s, i) => 
        [a.datasets[0].backgroundColor, a.datasets[0].data, a.labels][i].push(s)
      );
      return a
    }, {
      labels: [],
      datasets: [{
        backgroundColor: [],
        data: [],
        borderColor: 'rgba(22,22,22,0.3)',
        borderWidth: 1
      }]
    })
  }
}"/>
</p>

<br>

# Top Mods Details (except JEI, FML and Forge)
<p align="center">
<img src="https://quickchart.io/chart?w=400&h=450&c={
  options: {
    scales: {
      xAxes: [{stacked: true}],
      yAxes: [{stacked: true}],
    },
    plugins: {
      datalabels: {
        anchor: 'end',
        align: 'top',
        color: 'white',
        backgroundColor: 'rgba(46, 140, 171, 0.6)',
        borderColor: 'rgba(41, 168, 194, 1.0)',
        borderWidth: 0.5,
        borderRadius: 3,
        padding: 0,
        font: {size:10},
        formatter: (v,ctx) => 
          ctx.datasetIndex!=ctx.chart.data.datasets.length-1 ? null
            : [((ctx.chart.data.datasets.reduce((a,b)=>a- -b.data[ctx.dataIndex],0)*10)|0)/10,'s'].join('')
      },
      colorschemes: {
        scheme: 'office.Damask6'
      }
    }
  },
  type: 'bar',
  data: {...(() => {
    let a = { labels: [], datasets: [] };
`
1: Construction;
2: Loading Resources;
3: PreInitialization;
4: Initialization;
5: InterModComms$IMC;
6: PostInitialization;
7: LoadComplete;
8: ModIdMapping
`
    .split(';')
      .map(l => l.match(/\d: (.*)/).slice(1))
      .forEach(([name]) => a.datasets.push({ label: name, data: [] }));
`
                        1      2      3      4      5      6      7      8  ;
OpenComputers       |  0.14|  0.00|  3.80|  1.81|  0.00|  0.00|  0.00|  0.00;
Astral Sorcery      |  0.18|  0.00|  4.19|  0.80|  0.00|  0.00|  0.00|  0.00;
IndustrialCraft 2   |  0.85|  0.00|  3.37|  0.50|  0.00|  0.00|  0.00|  0.00;
Ender IO            |  1.54|  0.00|  2.57|  0.21|  0.00|  0.00|  0.00|  0.00;
NuclearCraft        |  0.05|  0.00|  2.97|  0.22|  0.00|  0.00|  0.00|  0.00;
CraftTweaker2       |  0.13|  0.00|  2.61|  0.00|  0.00|  0.00|  0.00|  0.00;
Forestry            |  0.29|  0.00|  1.87|  0.36|  0.00|  0.00|  0.00|  0.00;
Quark: RotN Edition |  0.02|  0.00|  2.42|  0.05|  0.00|  0.00|  0.00|  0.00;
Integrated Dynamics |  0.13|  0.00|  2.27|  0.05|  0.00|  0.00|  0.00|  0.00;
Cyclic              |  0.04|  0.00|  1.69|  0.35|  0.00|  0.00|  0.00|  0.00;
Extra Utilities 2   |  0.05|  0.00|  1.93|  0.02|  0.00|  0.00|  0.00|  0.00;
The Twilight Forest |  0.77|  0.00|  1.09|  0.11|  0.00|  0.00|  0.00|  0.00
`
    .split(';').slice(1)
      .map(l => l.split('|').map(s => s.trim()))
      .forEach(([name, ...arr], i) => {
        a.labels.push(name);
        arr.forEach((v, j) => a.datasets[j].data[i] = v)
      }); return a
  })()}
}"/>
</p>

<br>

# TOP JEI Registered Plugis
<p align="center">
<img src="https://quickchart.io/chart?w=700&c={
  options: {
    elements: { rectangle: { borderWidth: 1 } },
    legend: false
  },
  type: 'horizontalBar',
    data: {...(() => {
      let a = {
        labels: [], datasets: [{
          backgroundColor: 'rgba(0, 99, 132, 0.5)',
          borderColor: 'rgb(0, 99, 132)',
          data: []
        }]
      };
`
  1.42: jeresources.jei.JEIConfig;
  0.84: com.rwtema.extrautils2.crafting.jei.XUJEIPlugin;
  0.46: crazypants.enderio.machines.integration.jei.MachinesPlugin;
  0.37: ic2.jeiIntegration.SubModule;
  0.32: com.buuz135.industrial.jei.JEICustomPlugin;
  0.30: mezz.jei.plugins.vanilla.VanillaPlugin;
  0.24: crazypants.enderio.base.integration.jei.JeiPlugin;
  0.17: cofh.thermalexpansion.plugins.jei.JEIPluginTE;
  0.17: com.buuz135.thaumicjei.ThaumcraftJEIPlugin;
  0.16: knightminer.tcomplement.plugin.jei.JEIPlugin;
  0.13: p455w0rd.danknull.integration.JEI;
  0.13: ninjabrain.gendustryjei.GendustryJEIPlugin;
  0.10: net.bdew.jeibees.BeesJEIPlugin;
  0.07: crafttweaker.mods.jei.JEIAddonPlugin;
  0.07: lach_01298.qmd.jei.QMDJEI;
  1.36: Other 128 Plugins
`
        .split(';')
        .map(l => l.split(':'))
        .forEach(([time, name]) => {
          a.labels.push(name);
          a.datasets[0].data.push(time)
        })
        ; return a
    })()
  }
}"/>
</p>

<br>

# FML Stuff
<p align="center">
<img src="https://quickchart.io/chart?w=500&h=400&c={
  options: {
    rotation: Math.PI,
    cutoutPercentage: 55,
    plugins: {
      legend: !1,
      outlabels: {
        stretch: 5,
        padding: 1,
        text: (v)=>v.labels
      },
      doughnutlabel: {
        labels: [
          {
            text: 'FML stuff:',
            color: 'rgba(128, 128, 128, 0.5)',
            font: {size: 18}
          },
          {
            text: [160.55,'s'].join(''),
            color: 'rgba(128, 128, 128, 1)',
            font: {size: 22}
          }
        ]
      },
    }
  },
  type: 'outlabeledPie',
  data: {...(() => {
    let a = {
      labels: [],
      datasets: [{
        backgroundColor: [],
        data: [],
        borderColor: 'rgba(22,22,22,0.3)',
        borderWidth: 2
      }]
    };
`
993A00   0.42s Loading sounds;
994400   0.45s Loading Resource - SoundHandler;
444444 159.69s Other
`
    .split(';')
      .map(l => l.match(/(\w{6}) *(\d*\.\d*)s (.*)/))
      .forEach(([, col, time, name]) => {
        a.labels.push([name, ' ', time, 's'].join(''));
        a.datasets[0].data.push(parseFloat(time));
        a.datasets[0].backgroundColor.push([String.fromCharCode(35), col].join(''))
      })
      ; return a
  })()}
}"/>
</p>

<br>

## Minecraft load time benchmark


---

<p align="center" style="font-size:160%;">
MC total load time:<br>
354.03 sec
<br>
<sup><sub>(
5:54 min
)</sub></sup>
</p>

<br>


<p align="center">
<img src="https://quickchart.io/chart?w=400&h=30&c={
  type: 'horizontalBar',
  data: {
    datasets: [
      {label:      'MODS:', data: [119.96]},
      {label: 'FML stuff:', data: [234.07]}
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
8f304e   5.68s Astral Sorcery;
813e81   5.52s OpenComputers;
a651a8   4.70s IndustrialCraft 2;
516fa8   4.60s Ender IO;
213664   3.10s Forestry;
642136   3.05s FTB Quests;
cd922c   2.99s NuclearCraft;
308f7e   2.87s Quark: RotN Edition;
30518f   2.85s Patchouli;
5161a8   2.85s CraftTweaker2;
495797   9.44s CraftTweaker2 (Script Loading);
3e8160   2.37s The Twilight Forest;
ba3eb8   2.24s Cyclic;
436e17   2.23s Integrated Dynamics;
8c2ccd   2.03s Immersive Engineering;
95219e   1.88s ContentTweaker;
a86e51   1.83s Extra Utilities 2;
3e68ba   1.78s AE2 Unofficial Extended Life;
3eb2ba   1.72s Botania;
8f4d30   1.57s Open Terrain Generator;
813e80   1.56s Shadowfacts' Forgelin (Dummy);
444444  14.48s 12 Other mods;
333333  39.25s 135 'Fast' mods (load 1.0s - 0.1s);
222222   8.82s 300 'Instant' mods (load %3C 0.1s)
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
Astral Sorcery      |  0.18|  0.00|  4.89|  0.61|  0.00|  0.00|  0.00|  0.00;
OpenComputers       |  0.14|  0.01|  3.52|  1.85|  0.00|  0.00|  0.00|  0.00;
IndustrialCraft 2   |  0.84|  0.00|  3.40|  0.46|  0.00|  0.00|  0.00|  0.00;
Ender IO            |  1.27|  0.00|  3.15|  0.18|  0.00|  0.00|  0.00|  0.00;
Forestry            |  0.53|  0.00|  2.21|  0.36|  0.00|  0.00|  0.00|  0.00;
FTB Quests          |  0.16|  0.00|  2.90|  0.00|  0.00|  0.00|  0.00|  0.00;
NuclearCraft        |  0.05|  0.00|  2.73|  0.21|  0.00|  0.00|  0.00|  0.00;
Quark: RotN Edition |  0.02|  0.00|  2.78|  0.07|  0.00|  0.00|  0.00|  0.00;
Patchouli           |  0.02|  0.00|  2.81|  0.01|  0.00|  0.00|  0.00|  0.00;
CraftTweaker2       |  0.13|  0.00|  2.71|  0.00|  0.00|  0.00|  0.00|  0.00;
The Twilight Forest |  0.65|  0.00|  1.61|  0.11|  0.00|  0.00|  0.00|  0.00;
Cyclic              |  0.04|  0.00|  1.82|  0.38|  0.00|  0.00|  0.00|  0.00
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
  1.75: jeresources.jei.JEIConfig;
  0.96: com.rwtema.extrautils2.crafting.jei.XUJEIPlugin;
  0.53: crazypants.enderio.machines.integration.jei.MachinesPlugin;
  0.42: mezz.jei.plugins.vanilla.VanillaPlugin;
  0.41: com.buuz135.industrial.jei.JEICustomPlugin;
  0.36: knightminer.tcomplement.plugin.jei.JEIPlugin;
  0.35: ic2.jeiIntegration.SubModule;
  0.30: ninjabrain.gendustryjei.GendustryJEIPlugin;
  0.27: crazypants.enderio.base.integration.jei.JeiPlugin;
  0.24: com.buuz135.thaumicjei.ThaumcraftJEIPlugin;
  0.20: cofh.thermalexpansion.plugins.jei.JEIPluginTE;
  0.12: crafttweaker.mods.jei.JEIAddonPlugin;
  0.08: appeng.integration.modules.jei.JEIPlugin;
  0.08: forestry.factory.recipes.jei.FactoryJeiPlugin;
  0.08: net.bdew.jeibees.BeesJEIPlugin;
  1.45: Other 126 Plugins
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
            text: [234.07,'s'].join(''),
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
993A00   8.84s Loading sounds;
994400   8.89s Loading Resource - SoundHandler;
444444 216.34s Other
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

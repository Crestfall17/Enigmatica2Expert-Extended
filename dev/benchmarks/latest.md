## Minecraft load time benchmark

---

<p align="center" style="font-size:160%;">
MC total load time:<br>
247 sec
<br>
<sup><sub>(
4:07 min
)</sub></sup>
</p>

<br>
<!--
Note for image scripts:
  - Newlines are ignored
  - This characters cant be used: +<"%#
-->
<p align="center">
<img src="https://quickchart.io/chart.png?w=400&h=60&c={
  type: 'horizontalBar',
  data: {
    datasets: [
        {label: 'Mixins\n', data: [26.00]},
        {label: 'Construction\n', data: [51.00]},
        {label: 'PreInit\n', data: [118.00]},
        {label: 'Init\n', data: [49.00]},
    ]
  },
  options: {
    layout: { padding: { top: 10 } },
    scales: {
      xAxes: [{display: false, stacked: true}],
      yAxes: [{display: false, stacked: true}],
    },
    elements: {rectangle: {borderWidth: 2}},
    legend: {display: false},
    plugins: {datalabels: {
      color: 'white',
      font: {
        family: 'Consolas',
      },
      formatter: (value, context) =>
        [context.dataset.label, value, 's'].join('')
    }},
    annotation: {
      clip: false,
      annotations: [{
          type: 'line',
          scaleID: 'x-axis-0',
          value: 26,
          borderColor: 'black',
          label: {
            content: 'Window appear',
            fontSize: 8,
            enabled: true,
            xPadding: 8, yPadding: 2,
            yAdjust: -20
          },
        }
      ]
    },
  }
}"/>
</p>

<br>

# Mods Loading Time

<p align="center">
<img src="https://quickchart.io/chart.png?w=400&h=300&c={
  type: 'outlabeledPie',
  options: {
    rotation: Math.PI,
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
5161a8  6.62s CraftTweaker2;
436e17  6.39s Had Enough Items;
395E14  1.34s [JEI Ingredient Filter];
395E14  7.00s [JEI Plugins];
516fa8  6.15s Ender IO;
8f304e  5.36s Astral Sorcery;
a651a8  4.89s IndustrialCraft 2;
6e5e17  4.67s Tinkers' Antique;
5E5014  3.00s [TCon Textures];
cd922c  3.33s NuclearCraft;
6e175e  3.09s Recurrent Complex;
813e81  2.88s OpenComputers;
213664  2.86s Forestry;
308f7e  2.52s Quark: RotN Edition;
216364  2.42s Thermal Expansion;
306e8f  2.04s Custom Loading Screen;
ba3eb8  2.04s Cyclic;
436e17  1.99s Integrated Dynamics;
3e7d81  1.98s ProbeZS;
444444 23.97s 17 Other mods;
333333 44.84s 142 'Fast' mods (1.0s - 0.1s);
222222  7.74s 308 'Instant' mods (%3C 0.1s)
`
    .split(';').reduce((a, l) => {
      l.match(/(\w{6}) *(\d*\.\d*) ?s (.*)/s)
      .slice(1).map((a, i) => [[String.fromCharCode(35),a].join(''), a,
        a.length > 15 ? a.split(/(?%3C=.{9})\s(?=\S{5})/).join('\n') : a
      ][i])
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

# Loader steps

Show how much time each mod takes on each game load phase.

JEI/HEI not included, since its load time based on other mods and overal item count.

<p align="center">
<img src="https://quickchart.io/chart.png?w=400&h=450&c={
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
0: Construction;
1: Loading Resources;
2: PreInitialization;
3: Initialization;
4: InterModComms;
5: LoadComplete;
6: ModIdMapping;
7: Other
`
    .split(';')
      .map(l => l.match(/\d: (.*)/).slice(1))
      .forEach(([name]) => a.datasets.push({ label: name, data: [] }));
`
                                  0      1      2      3      4      5      6      7;
CraftTweaker2                 | 0.12| 0.00| 2.42| 4.01| 0.00| 0.08| 0.00| 0.00;
Ender IO                      | 1.60| 0.01| 2.88| 0.27| 1.38| 0.00| 0.01| 0.00;
Astral Sorcery                | 0.19| 0.00| 4.27| 0.91| 0.00| 0.00| 0.00| 0.00;
IndustrialCraft 2             | 0.72| 0.01| 3.31| 0.85| 0.00| 0.00| 0.00| 0.00;
Tinkers' Antique              | 0.83| 0.01| 0.10| 0.73| 0.00| 0.00| 0.00| 3.00;
NuclearCraft                  | 0.05| 0.01| 2.37| 0.89| 0.00| 0.00| 0.03| 0.00;
Recurrent Complex             | 0.16| 0.00| 0.28| 2.65| 0.00| 0.00| 0.00| 0.00;
OpenComputers                 | 0.18| 0.01| 1.30| 1.35| 0.04| 0.00| 0.00| 0.00;
Forestry                      | 0.33| 0.01| 1.96| 0.57| 0.00| 0.00| 0.00| 0.00;
Quark: RotN Edition           | 0.02| 0.01| 2.39| 0.11| 0.00| 0.00| 0.00| 0.00;
[Mod Average]                 | 0.06| 0.00| 0.14| 0.07| 0.00| 0.00| 0.00| 0.01
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
<img src="https://quickchart.io/chart.png?w=500&h=200&c={
  options: {
    elements: { rectangle: { borderWidth: 1 } },
    legend: false,
    scales: {
      yAxes: [{ ticks: { fontSize: 9, fontFamily: 'Verdana' }}],
    },
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
 1.26: li.cil.oc.integration.jei.ModPluginOpenComputers;
 0.75: jeresources.jei.JEIConfig;
 0.72: com.rwtema.extrautils2.crafting.jei.XUJEIPlugin;
 0.57: ic2.jeiIntegration.SubModule;
 0.54: crazypants.enderio.machines.integration.jei.MachinesPlugin;
 0.47: mezz.jei.plugins.vanilla.VanillaPlugin;
 0.34: com.buuz135.industrial.jei.JEICustomPlugin;
 0.17: knightminer.tcomplement.plugin.jei.JEIPlugin;
 0.16: cofh.thermalexpansion.plugins.jei.JEIPluginTE;
 0.16: crazypants.enderio.base.integration.jei.JeiPlugin;
 0.15: com.buuz135.thaumicjei.ThaumcraftJEIPlugin;
 0.13: rustic.compat.jei.RusticJEIPlugin;
 1.58: Other
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

Loading bars that usually not related to specific mods.

⚠️ Shows only steps that took 1.0 sec or more.

<p align="center">
<img src="https://quickchart.io/chart.png?w=500&h=400&c={
  options: {
    rotation: Math.PI*1.125,
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
            text: '100.12s',
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
994400  1.35s Reloading;
001799  2.54s Loading Resource - AssetLibrary;
229900  2.88s Preloading 51458 textures;
179900  1.51s Texture loading;
00991C  3.79s Posting bake events;
009926 27.74s Setting up dynamic models;
009930 27.80s Loading Resource - ModelManager;
009996 28.72s Rendering Setup;
440099  1.33s XML Recipes;
4F0099  1.93s InterModComms;
99007D 11.96s [VintageFix]: Texture search 69580 sprites;
990073  2.94s Preloaded 33710 sprites
`
    .split(';')
      .map(l => l.match(/(\w{6}) *(\d*\.\d*) ?s (.*)/s))
      .forEach(([, col, time, name]) => {
        a.labels.push([
          name.length > 15 ? name.split(/(?%3C=.{11})\s(?=\S{6})/).join('\n') : name
          , ' ', time, 's'
        ].join(''));
        a.datasets[0].data.push(parseFloat(time));
        a.datasets[0].backgroundColor.push([String.fromCharCode(35), col].join(''))
      })
      ; return a
  })()}
}"/>
</p>

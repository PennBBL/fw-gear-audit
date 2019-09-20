# `fw-gear-audit`
A Python SDK tool for auditing gear run data

Use this tool to fetch data from Flywheel describing which gears have been run within a project and how they were configured. You can also join SeqInfo data to help filter your data by sequences.

```
usage: FlywheelGearAudit.py [-h] --project PROJECT [PROJECT ...]
                            [--subject SUBJECT [SUBJECT ...]]
                            [--session SESSION [SESSION ...]] [--verbose]
                            [--dry_run] (--path PATH | --fname FNAME)
                            (--by-runs | --by-sequences)
```

# Goal
You can run many analysis gears on Flywheel. Keeping track of these within a subject is easy with the GUI, but to view this data en masse requires the use of the SDK to loop over each subject and collect their gear run data. This becomes troublesome when, for example with fMRIPrep, there can be many runs of the same gear due to version updates, feature testing, incorrect configs, or random errors causing gears to crash.

This leaves users in a situation where they may not be sure if the correct version and configuration of fMRIPrep was run successfully for 100% of the participants in their 200-cohort study.

`fw-gear-audit` aims to remedy this situation by quickly and efficiently gathering data about gear runs and providing the user with a tabular `.csv` file for their records.

# Features

* Use the `--subject` and `--session` flags to filter your data within project by subject or session labels. 
* By default, gear run data includes the gear name, version, runtime and date, and completion status. Use the `--verbose` flag to output both gear run data and configuration information for each run
* Choose between `--by-runs` to output a table where each row is a gear run, or `--by-sequences` to output a table where each gear run is accompanied by a `seqInfo` subtable

## By Run:

**subject**|**session**|**gearName**|**gearVersion**|**runLabel**|**runDatetime**|**runRuntimeMS**|**runStatus**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed
104059|10762|fmriprep125|0.1.7\_1.2.5|fmriprep\_SDK\_010762\_2019-04-22\_17:32|2019-04-22 21:33:25.870000+00:00|14055|failed
104059|10762|fmriprep125|0.1.7\_1.2.5|fmriprep\_SDK\_010762\_2019-04-24\_11:31|2019-04-24 15:36:34.178000+00:00|287719|failed
104059|10762|fmriprep125|0.1.7\_1.2.5|fmriprep\_SDK\_010762\_2019-04-24\_16:45|2019-04-24 20:45:21.188000+00:00|55392635|complete
104059|10762|xcpengine-fw|1.063|XCP\_SDK 2019-05-17 11:35:54.021070|2019-05-17 15:35:54.085000+00:00|5553043|complete
104059|10762|xcpengine-fw|1.0633|XCP\_SDK 2019-06-17 16:44:12.682716|2019-06-17 20:44:12.754000+00:00|312121575|failed
104059|10762|xcpengine-fw|1.06338|XCP\_SDK\_task\_module\_2019-06-26 13:08:13.199392|2019-06-26 17:08:13.274000+00:00|28015|complete
104059|10762|xcpengine-fw|1.06338|XCP\_SDK\_taskregress\_module\_2019-06-26 19:10:02|2019-06-26 19:10:02.888000+00:00|27375|complete
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_11196|2019-04-15 20:45:35.356000+00:00|44505363|failed
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_11196|2019-04-16 16:27:13.458000+00:00|44010936|failed
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/17/2019 11:33:10|2019-04-17 15:33:57.530000+00:00|30092|failed
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/17/2019 12:36:44|2019-04-17 16:37:15.579000+00:00|73098331|complete
86486|11196|fmriprep125|0.1.7\_1.2.5|fmriprep\_SDK\_11196\_2019-04-22\_17:32|2019-04-22 21:33:36.983000+00:00|16347|failed
86486|11196|fmriprep125|0.1.7\_1.2.5|fmriprep125 04/23/2019 16:07:28|2019-04-23 20:07:49.717000+00:00|17150|failed
86486|11196|fmriprep125|0.1.7\_1.2.5|fmriprep125 04/23/2019 16:17:26|2019-04-23 20:17:45.532000+00:00|65726568|complete
86486|11196|fmriprep125|0.1.7\_1.2.5|fmriprep\_SDK\_11196\_2019-04-24\_11:31|2019-04-24 15:36:42.723000+00:00|52406897|complete
86486|11196|xcpengine-fw|1.063|xcpengine-fw 04/27/2019 19:33:41|2019-04-27 23:34:13.359000+00:00|4775298|complete
86486|11196|fw-heudiconv|0.1.11\_0.1.0|fw-heudiconv 05/10/2019 15:14:42|2019-05-10 19:14:57.904000+00:00|14759|complete
86486|11196|xcpengine-fw|1.063|xcpengine-fw 05/15/2019 10:37:09|2019-05-15 14:37:37.681000+00:00|320600623|complete
86486|11196|xcpengine-fw|1.063|xcpengine-fw 05/15/2019 10:37:44|2019-05-15 14:43:11.425000+00:00|318911954|complete
86486|11196|xcpengine-fw|1.063|xcpenginestruct 05/25/2019 19:14:49|2019-05-25 23:15:35.105000+00:00|322438769|complete
86486|11196|xcpengine-fw|1.0631|xcpengine-fw 06/13/2019 12:59:24|2019-06-13 17:00:03.867000+00:00|1457|failed
86486|11196|xcpengine-fw|1.0633|XCP\_SDK 2019-06-17 16:45:31.934948|2019-06-17 20:45:32.002000+00:00|316570122|failed
86486|11196|xcpengine-fw|1.06336|xcpengine-fw 06/25/2019 14:50:03|2019-06-25 18:50:46.914000+00:00|31014|complete
86486|11196|xcpengine-fw|1.06337|xcpengine-fw 06/25/2019 15:41:09|2019-06-25 19:42:04.137000+00:00|1030893|complete
86486|11196|xcpengine-fw|1.06337|xcpengine-fw 06/25/2019 15:56:22|2019-06-25 19:57:17.108000+00:00|1534523|complete
86486|11196|xcpengine-fw|1.06338|XCP\_SDK\_task\_module\_2019-06-26 13:08:18.700338|2019-06-26 17:08:18.774000+00:00|1562030|complete
86486|11196|xcpengine-fw|1.06338|XCP\_SDK\_taskregress\_module\_2019-06-26 19:10:09|2019-06-26 19:10:09.688000+00:00|1031698|complete
86486|11196|xcpengine-fw|1.06339|xcpengine-fw 07/02/2019 12:38:10|2019-07-02 16:39:02.284000+00:00|1292985|complete

This allows you to filter, for e.g., which subjects successfully ran XCPEngine with version 1.06338
```
# Tidy R syntax:
df %>% 
  filter(str_detect(gearName, 'xcpengine')) %>% 
  filter(str_detect(runStatus, 'complete')) %>%
  filter(str_detect(gearVersion, '6338'))
```

## By Sequences

This option creates a data frame where each run above is also joined by a sequence info table for that participant:

**subject**|**session**|**gearName**|**gearVersion**|**runLabel**|**runDatetime**|**runRuntimeMS**|**runStatus**|**seriesID**|**dcmDirName**|**dim1**|**dim2**|**dim3**|**dim4**|**TR**|**TE**|**protocolName**|**isMotionCorrected**|**isDerived**|**seriesDescription**|**sequenceName**|**imageType**|**seriesUid**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c75633aba2580002d3902e6|Localizer\_1\_i00003.nii.gz|512|512|3|-1|0.0086|0.004|Localizer|False|False|Localizer|\_fl2d1|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814140178131880096.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c75633aba2580002d3902e6|Localizer\_1\_i00002.nii.gz|512|512|3|-1|0.0086|0.004|Localizer|False|False|Localizer|\_fl2d1|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814140178131880096.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c75633aba2580002d3902e6|Localizer\_1\_i00001.nii.gz|512|512|3|-1|0.0086|0.004|Localizer|False|False|Localizer|\_fl2d1|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814140178131880096.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba25800038398297|restingBOLD\_mb6\_1200\_10.nii.gz|448|448|1200|-1|0.5|0.025|restingBOLD\_mb6\_1200|False|False|restingBOLD\_mb6\_1200|epfid2d1\_64|('ORIGINAL', 'PRIMARY', 'M', 'MB', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.201804181426368296184317.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba25800038398298|bbl1\_restbold1\_124mb\_11.nii.gz|448|448|124|-1|3|0.032|bbl1\_restbold1\_124mb|False|False|bbl1\_restbold1\_124mb|epfid2d1\_64|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.2018041814370267454559619.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba2580003939a503|ASL\_3DSPIRAL\_V20\_GE\_12\_Eq\_1.nii.gz|64|64|64|-1|0.022|0.01003| |False|False| | |()| 
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba2580003939a503|ASL\_3DSPIRAL\_V20\_GE\_12.nii.gz|64|64|64|-1|4.6255|0.01003|ASL\_3DSPIRAL\_V20\_GE|False|False|ASL\_3DSPIRAL\_V20\_GE\_M0|Sp3d1|('ORIGINAL', 'PRIMARY', 'M', 'ND')|1.3.12.2.1107.5.2.43.66044.2018041814445154289476985.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba25800038398296|ASL\_3DSPIRAL\_V20\_GE\_13.nii.gz|64|64|2560|-1|4.6255|0.01003|ASL\_3DSPIRAL\_V20\_GE|False|False|ASL\_3DSPIRAL\_V20\_GE\_ASL|Sp3d1|('ORIGINAL', 'PRIMARY', 'M', 'ND')|1.3.12.2.1107.5.2.43.66044.2018041814445430648677051.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba2580002e38dd54|ASL\_3DSPIRAL\_V20\_GE\_14.nii.gz|64|64|32|-1|4.6255|0.01003|ASL\_3DSPIRAL\_V20\_GE|False|False|ASL\_3DSPIRAL\_V20\_GE\_MeanPerf|Sp3d1|('ORIGINAL', 'PRIMARY', 'M', 'ND')|1.3.12.2.1107.5.2.43.66044.2018041814445154291576986.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba2580002c38d5df|DTI\_MultiShell\_117dir\_15.nii.gz|1400|1400|118|-1|3.027|0.0828|DTI\_MultiShell\_117dir|False|False|DTI\_MultiShell\_117dir|ep\_b5#1|('ORIGINAL', 'PRIMARY', 'DIFFUSION', 'NONE', 'MB', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.2018041814510448864779646.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba2580002c38d5df|DTI\_MultiShell\_117dir\_15.bvec|1400|1400|118|-1|3.027|0.0828|DTI\_MultiShell\_117dir|False|False|DTI\_MultiShell\_117dir|ep\_b5#1|('ORIGINAL', 'PRIMARY', 'DIFFUSION', 'NONE', 'MB', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.2018041814510448864779646.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba2580002c38d5df|DTI\_MultiShell\_117dir\_15.bval|1400|1400|118|-1|3.027|0.0828|DTI\_MultiShell\_117dir|False|False|DTI\_MultiShell\_117dir|ep\_b5#1|('ORIGINAL', 'PRIMARY', 'DIFFUSION', 'NONE', 'MB', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.2018041814510448864779646.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba25800038398294|DTI\_MultiShell\_topup\_ref\_17.nii.gz|140|140|92|-1|3.027|0.0828|DTI\_MultiShell\_topup\_ref|False|False|DTI\_MultiShell\_topup\_ref|ep\_b5#1|('ORIGINAL', 'PRIMARY', 'DIFFUSION', 'NONE', 'MB', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814573463580034910.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba25800038398299|MPRAGE\_TI1100\_ipat2\_2.nii.gz|256|192|160|-1|1.81|0.00345|MPRAGE\_TI1100\_ipat2|False|False|MPRAGE\_TI1100\_ipat2|\_tfl3d1\_16|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814150078639280942.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba2580003939a505|T2\_sagittal\_SPACE\_3.nii.gz|256|256|176|-1|3.2|0.408|T2\_sagittal\_SPACE|False|False|T2\_sagittal\_SPACE|\_spc\_282ns|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814225838675681811.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c75633aba2580002e38dd55|TOF\_3D\_multi-slab\_R2\_4.nii.gz|384|288|74|-1|0.022|0.00366|TOF\_3D\_multi-slab\_R2|False|False|TOF\_3D\_multi-slab\_R2|\_fl3d1r\_t70|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814230724412383000.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba2580003839829a|TOF\_3D\_multi-slab\_R2\_5.nii.gz|142|384|1|-1|0.022|0.00366|TOF\_3D\_multi-slab\_R2|False|False|TOF\_3D\_multi-slab\_R2\_MIP\_SAG|\_fl3d1r\_t70|('ORIGINAL', 'PRIMARY', 'MIP', 'SAG', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814244435763483338.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c75633aba2580003839829b|TOF\_3D\_multi-slab\_R2\_6.nii.gz|142|288|1|-1|0.022|0.00366|TOF\_3D\_multi-slab\_R2|False|False|TOF\_3D\_multi-slab\_R2\_MIP\_COR|\_fl3d1r\_t70|('ORIGINAL', 'PRIMARY', 'MIP', 'COR', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814244435762983336.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c75633aba2580002a38c710|TOF\_3D\_multi-slab\_R2\_7.nii.gz|384|288|1|-1|0.022|0.00366|TOF\_3D\_multi-slab\_R2|False|False|TOF\_3D\_multi-slab\_R2\_MIP\_TRA|\_fl3d1r\_t70|('ORIGINAL', 'PRIMARY', 'MIP', 'TRA', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814244435762083334.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba2580003939a504|B0map\_8\_e2.nii.gz|80|80|120|-1|0.58|0.00658|B0map|False|False|B0map|\_fm2d2r|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814245128954183710.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba2580003939a504|B0map\_8\_e1.nii.gz|80|80|120|-1|0.58|0.00412|B0map|False|False|B0map|\_fm2d2r|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814245128954183710.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-15 20:45:24.774000+00:00|63361|failed|5c756339ba2580002c38d5e0|B0map\_9\_ph.nii.gz|80|80|60|-1|0.58|0.00658|B0map|False|False|B0map|\_fm2d2r|('ORIGINAL', 'PRIMARY', 'P', 'ND')|1.3.12.2.1107.5.2.43.66044.2018041814245128955483711.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c75633aba2580002d3902e6|Localizer\_1\_i00003.nii.gz|512|512|3|-1|0.0086|0.004|Localizer|False|False|Localizer|\_fl2d1|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814140178131880096.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c75633aba2580002d3902e6|Localizer\_1\_i00002.nii.gz|512|512|3|-1|0.0086|0.004|Localizer|False|False|Localizer|\_fl2d1|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814140178131880096.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c75633aba2580002d3902e6|Localizer\_1\_i00001.nii.gz|512|512|3|-1|0.0086|0.004|Localizer|False|False|Localizer|\_fl2d1|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814140178131880096.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba25800038398297|restingBOLD\_mb6\_1200\_10.nii.gz|448|448|1200|-1|0.5|0.025|restingBOLD\_mb6\_1200|False|False|restingBOLD\_mb6\_1200|epfid2d1\_64|('ORIGINAL', 'PRIMARY', 'M', 'MB', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.201804181426368296184317.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba25800038398298|bbl1\_restbold1\_124mb\_11.nii.gz|448|448|124|-1|3|0.032|bbl1\_restbold1\_124mb|False|False|bbl1\_restbold1\_124mb|epfid2d1\_64|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.2018041814370267454559619.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba2580003939a503|ASL\_3DSPIRAL\_V20\_GE\_12\_Eq\_1.nii.gz|64|64|64|-1|0.022|0.01003| |False|False| | |()| 
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba2580003939a503|ASL\_3DSPIRAL\_V20\_GE\_12.nii.gz|64|64|64|-1|4.6255|0.01003|ASL\_3DSPIRAL\_V20\_GE|False|False|ASL\_3DSPIRAL\_V20\_GE\_M0|Sp3d1|('ORIGINAL', 'PRIMARY', 'M', 'ND')|1.3.12.2.1107.5.2.43.66044.2018041814445154289476985.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba25800038398296|ASL\_3DSPIRAL\_V20\_GE\_13.nii.gz|64|64|2560|-1|4.6255|0.01003|ASL\_3DSPIRAL\_V20\_GE|False|False|ASL\_3DSPIRAL\_V20\_GE\_ASL|Sp3d1|('ORIGINAL', 'PRIMARY', 'M', 'ND')|1.3.12.2.1107.5.2.43.66044.2018041814445430648677051.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba2580002e38dd54|ASL\_3DSPIRAL\_V20\_GE\_14.nii.gz|64|64|32|-1|4.6255|0.01003|ASL\_3DSPIRAL\_V20\_GE|False|False|ASL\_3DSPIRAL\_V20\_GE\_MeanPerf|Sp3d1|('ORIGINAL', 'PRIMARY', 'M', 'ND')|1.3.12.2.1107.5.2.43.66044.2018041814445154291576986.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba2580002c38d5df|DTI\_MultiShell\_117dir\_15.nii.gz|1400|1400|118|-1|3.027|0.0828|DTI\_MultiShell\_117dir|False|False|DTI\_MultiShell\_117dir|ep\_b5#1|('ORIGINAL', 'PRIMARY', 'DIFFUSION', 'NONE', 'MB', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.2018041814510448864779646.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba2580002c38d5df|DTI\_MultiShell\_117dir\_15.bvec|1400|1400|118|-1|3.027|0.0828|DTI\_MultiShell\_117dir|False|False|DTI\_MultiShell\_117dir|ep\_b5#1|('ORIGINAL', 'PRIMARY', 'DIFFUSION', 'NONE', 'MB', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.2018041814510448864779646.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba2580002c38d5df|DTI\_MultiShell\_117dir\_15.bval|1400|1400|118|-1|3.027|0.0828|DTI\_MultiShell\_117dir|False|False|DTI\_MultiShell\_117dir|ep\_b5#1|('ORIGINAL', 'PRIMARY', 'DIFFUSION', 'NONE', 'MB', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.2018041814510448864779646.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba25800038398294|DTI\_MultiShell\_topup\_ref\_17.nii.gz|140|140|92|-1|3.027|0.0828|DTI\_MultiShell\_topup\_ref|False|False|DTI\_MultiShell\_topup\_ref|ep\_b5#1|('ORIGINAL', 'PRIMARY', 'DIFFUSION', 'NONE', 'MB', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814573463580034910.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba25800038398299|MPRAGE\_TI1100\_ipat2\_2.nii.gz|256|192|160|-1|1.81|0.00345|MPRAGE\_TI1100\_ipat2|False|False|MPRAGE\_TI1100\_ipat2|\_tfl3d1\_16|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814150078639280942.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba2580003939a505|T2\_sagittal\_SPACE\_3.nii.gz|256|256|176|-1|3.2|0.408|T2\_sagittal\_SPACE|False|False|T2\_sagittal\_SPACE|\_spc\_282ns|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814225838675681811.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c75633aba2580002e38dd55|TOF\_3D\_multi-slab\_R2\_4.nii.gz|384|288|74|-1|0.022|0.00366|TOF\_3D\_multi-slab\_R2|False|False|TOF\_3D\_multi-slab\_R2|\_fl3d1r\_t70|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814230724412383000.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba2580003839829a|TOF\_3D\_multi-slab\_R2\_5.nii.gz|142|384|1|-1|0.022|0.00366|TOF\_3D\_multi-slab\_R2|False|False|TOF\_3D\_multi-slab\_R2\_MIP\_SAG|\_fl3d1r\_t70|('ORIGINAL', 'PRIMARY', 'MIP', 'SAG', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814244435763483338.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c75633aba2580003839829b|TOF\_3D\_multi-slab\_R2\_6.nii.gz|142|288|1|-1|0.022|0.00366|TOF\_3D\_multi-slab\_R2|False|False|TOF\_3D\_multi-slab\_R2\_MIP\_COR|\_fl3d1r\_t70|('ORIGINAL', 'PRIMARY', 'MIP', 'COR', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814244435762983336.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c75633aba2580002a38c710|TOF\_3D\_multi-slab\_R2\_7.nii.gz|384|288|1|-1|0.022|0.00366|TOF\_3D\_multi-slab\_R2|False|False|TOF\_3D\_multi-slab\_R2\_MIP\_TRA|\_fl3d1r\_t70|('ORIGINAL', 'PRIMARY', 'MIP', 'TRA', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814244435762083334.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba2580003939a504|B0map\_8\_e2.nii.gz|80|80|120|-1|0.58|0.00658|B0map|False|False|B0map|\_fm2d2r|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814245128954183710.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba2580003939a504|B0map\_8\_e1.nii.gz|80|80|120|-1|0.58|0.00412|B0map|False|False|B0map|\_fm2d2r|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.2018041814245128954183710.0.0.0
104059|10762|fmriprep125|0.1.2\_1.2.5|fmriprep\_SDK\_010762|2019-04-16 16:27:02.664000+00:00|15829|failed|5c756339ba2580002c38d5e0|B0map\_9\_ph.nii.gz|80|80|60|-1|0.58|0.00658|B0map|False|False|B0map|\_fm2d2r|('ORIGINAL', 'PRIMARY', 'P', 'ND')|1.3.12.2.1107.5.2.43.66044.2018041814245128955483711.0.0.0
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93c0a6f546b6002abdfe43|1.3.12.2.1107.5.2.43.66044.30000019032116274975300004569.nii.gz|64|64|2560|-1|4|0.01003|ASL\_3DSPIRAL\_V20\_GE|False|False|ASL\_3DSPIRAL\_V20\_GE\_ASL|Sp3d1|('ORIGINAL', 'PRIMARY', 'M', 'ND')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300004569
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93be6df546b6002cbe1b65|1.3.12.2.1107.5.2.43.66044.30000019032116274975300002008\_Eq\_1.nii.gz|64|64|64|-1| | | |False|False| | |()| 
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93be6df546b6002cbe1b65|1.3.12.2.1107.5.2.43.66044.30000019032116274975300002008.nii.gz|64|64|64|-1|4|0.01003|ASL\_3DSPIRAL\_V20\_GE|False|False|ASL\_3DSPIRAL\_V20\_GE\_M0|Sp3d1|('ORIGINAL', 'PRIMARY', 'M', 'ND')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300002008
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93c0b0f546b6002fbf3a7e|1.3.12.2.1107.5.2.43.66044.30000019032116274975300004602.nii.gz|64|64|32|-1|4|0.01003|ASL\_3DSPIRAL\_V20\_GE|False|False|ASL\_3DSPIRAL\_V20\_GE\_MeanPerf|Sp3d1|('ORIGINAL', 'PRIMARY', 'M', 'ND')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300004602
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93bcebf546b6002cbe1b61|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000556\_e2.nii.gz|80|80|120|-1|0.58|0.00658|B0map|False|False|B0map|\_fm2d2r|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000556
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93bcebf546b6002cbe1b61|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000556\_e1.nii.gz|80|80|120|-1|0.58|0.00412|B0map|False|False|B0map|\_fm2d2r|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000556
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93bcfbf546b6002cbe1b63|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000617\_e2\_ph.nii.gz|80|80|60|-1|0.58|0.00658|B0map|False|False|B0map|\_fm2d2r|('ORIGINAL', 'PRIMARY', 'P', 'ND')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000617
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93c0f3f546b6002abdfe45|1.3.12.2.1107.5.2.43.66044.30000019032116274975300004721.nii.gz|1400|1400|118|-1|3.027|0.0828|DTI\_MultiShell\_117dir|False|False|DTI\_MultiShell\_117dir|ep\_b5#1|('ORIGINAL', 'PRIMARY', 'DIFFUSION', 'NONE', 'MB', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300004721
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93c0f3f546b6002abdfe45|1.3.12.2.1107.5.2.43.66044.30000019032116274975300004721.bvec|1400|1400|118|-1|3.027|0.0828|DTI\_MultiShell\_117dir|False|False|DTI\_MultiShell\_117dir|ep\_b5#1|('ORIGINAL', 'PRIMARY', 'DIFFUSION', 'NONE', 'MB', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300004721
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93c0f3f546b6002abdfe45|1.3.12.2.1107.5.2.43.66044.30000019032116274975300004721.bval|1400|1400|118|-1|3.027|0.0828|DTI\_MultiShell\_117dir|False|False|DTI\_MultiShell\_117dir|ep\_b5#1|('ORIGINAL', 'PRIMARY', 'DIFFUSION', 'NONE', 'MB', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300004721
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93c221f546b6002dbe38b3|1.3.12.2.1107.5.2.43.66044.30000019032116274975300005919.nii.gz|140|140|92|-1|3.027|0.0828|DTI\_MultiShell\_topup\_ref|False|False|DTI\_MultiShell\_topup\_ref|ep\_b5#1|('ORIGINAL', 'PRIMARY', 'DIFFUSION', 'NONE', 'MB', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300005919
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93bc57f546b6002ebe99b0|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000016\_i00003.nii.gz|512|512|3|-1|0.0086|0.004|Localizer|False|False|Localizer|\_fl2d1|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000016
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93bc57f546b6002ebe99b0|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000016\_i00002.nii.gz|512|512|3|-1|0.0086|0.004|Localizer|False|False|Localizer|\_fl2d1|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000016
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93bc57f546b6002ebe99b0|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000016\_i00001.nii.gz|512|512|3|-1|0.0086|0.004|Localizer|False|False|Localizer|\_fl2d1|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000016
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93bc82f546b6002abdfe33|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000177.nii.gz|256|192|160|-1|1.81|0.00345|MPRAGE\_TI1100\_ipat2|False|False|MPRAGE\_TI1100\_ipat2|\_tfl3d1\_16|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000177
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93bcaef546b6002fbf3a3c|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000354.nii.gz|256|256|176|-1|3.2|0.408|T2\_sagittal\_SPACE|False|False|T2\_sagittal\_SPACE|\_spc\_282ns|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000354
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93bcc3f546b6002fbf3a40|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000429.nii.gz|384|288|74|-1|0.022|0.00366|TOF\_3D\_multi-slab\_R2|False|False|TOF\_3D\_multi-slab\_R2|\_fl3d1r\_t70|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000429
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93bcc9f546b6002fbf3a45|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000433.nii.gz|142|288|1|-1|0.022|0.00366|TOF\_3D\_multi-slab\_R2|False|False|TOF\_3D\_multi-slab\_R2\_MIP\_COR|\_fl3d1r\_t70|('ORIGINAL', 'PRIMARY', 'MIP', 'COR', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000433
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93bcc6f546b6002abdfe35|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000431.nii.gz|142|384|1|-1|0.022|0.00366|TOF\_3D\_multi-slab\_R2|False|False|TOF\_3D\_multi-slab\_R2\_MIP\_SAG|\_fl3d1r\_t70|('ORIGINAL', 'PRIMARY', 'MIP', 'SAG', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000431
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93bcccf546b6002fbf3a49|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000435.nii.gz|384|288|1|-1|0.022|0.00366|TOF\_3D\_multi-slab\_R2|False|False|TOF\_3D\_multi-slab\_R2\_MIP\_TRA|\_fl3d1r\_t70|('ORIGINAL', 'PRIMARY', 'MIP', 'TRA', 'ND', 'NORM')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300000435
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93c261f546b6002abdfe49|1.3.12.2.1107.5.2.43.66044.30000019032116274975300006151.nii.gz|448|448|231|-1|3|0.032|bbl1\_fracback1\_231mb|False|False|bbl1\_fracback1\_231mb|epfid2d1\_64|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300006151
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93be5cf546b6002fbf3a50|1.3.12.2.1107.5.2.43.66044.30000019032116274975300001943.nii.gz|448|448|124|-1|3|0.032|bbl1\_restbold1\_124mb|False|False|bbl1\_restbold1\_124mb|epfid2d1\_64|('ORIGINAL', 'PRIMARY', 'M', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300001943
86486|11196|fmriprep125|0.1.2\_1.2.5|fmriprep125 04/05/2019 14:59:38|2019-04-05 19:00:04.294000+00:00|73752452|complete|5c93be3af546b6002ebe99ba|1.3.12.2.1107.5.2.43.66044.30000019032116274975300001818.nii.gz|448|448|1200|-1|0.5|0.025|restingBOLD\_mb6\_1200|False|False|restingBOLD\_mb6\_1200|epfid2d1\_64|('ORIGINAL', 'PRIMARY', 'M', 'MB', 'ND', 'NORM', 'MOSAIC')|1.3.12.2.1107.5.2.43.66044.30000019032116274975300001818

i.e. for every run, there is a full set of sequences, gathered/pivoted vertically. This long table now gives you the added option of filtering by sequence specific preconditions, e.g. any subject with a T1w image should have an fMRIPrep run:
```
# Tidy R syntax:
df %>% 
  filter(str_detect(tolower(gearName), 'fmriprep')) %>% 
  filter(str_detect(runStatus, 'complete')) %>%
  filter(str_detect(tolower(protocolName), 't1w'))
```

# Conclusion

`fw-gear-audit` allows users to get a tabular, indexable, searchable overview of the progress of gears run on Flywheel.

Please submit any bug reports, feature requests, or questions to the [issues page](https://github.com/PennBBL/fw-gear-audit/issues).
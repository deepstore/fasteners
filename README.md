# Fasteners

# Dependencies

```
$ yay -S opencv2
$ pipenv install
```

# CODE

- SXXX = Screw
- BXXX = Bolt
- NXXX = Nut

# 1. Data preparation

First of all, it's need to make directories by following cmd.

```
$ mkdir {datasets_raw}/xxx_dataset
$ # NOTE: datasets_vott will be crated by VoTT and Voc. and also datasets_voc will be copied from files exported by VoTT
```

# 2. VoTT Flow

do Annotion by VoTT

- Firstly, create Security Token and save it to somewhere private space
- Connections:
  - target connection
    - select local storage of datasets_vott/xxx_dataset
  - source connection
    - select local storage of datasets_raw/xxx_dataset
- Project settings
  - name is xxx_dataset
  - select security token and target/source connection that i have created
  - name is like `xxx_dataset_vott.vott` since there is already same name folder.
  - video frame rate is 1 sec
- Export Setings
  - providor: pascal voc
  - asset state: only tagged assets
  - tarinval:test = 80:20
  - export unsinged: check

after annotation is done, export proj as Pascal VOC

# 3. Copy exported Pascal VOC files to the datasets folder

```
$ co -R ./vott_targets/xxx_dataset/settings-PascalVOC-export/ ./datasets/xxx_dataset/
```

# 4. Auto Annotation and recreate xxx.txt

TODO

# 5. Convert Pascal VOC to YOLO Style

TODO

# CMD

```
$ python increase_img.py # before annotation for data augumentation
```

conv VoTT to YOLO

- aggregate all image ids to the trainval.txt and test.txt files from indivisual classname_train/val.txt which is created by VoTT.

```
$ python voc_summary.py 
```

- create lables files
- create test.txt from Main/test.txt and 
- create trainval.txt from Main/trainval.txt
- the difference between Main/xxx.txt and xxx.txt is that latter has image path and former has image id

```
$ python voc_label.py
```

# REFERENCES:

- https://github.com/wakuphas/wakuphas/blob/master/AI/Scripts/increase_img.py
- https://wakuphas.hatenablog.com/entry/2018/09/19/025941
- https://github.com/zchrissirhcz/imageset-viewer
- http://mukopikmin.hatenablog.com/entry/2018/12/05/002339
- https://github.com/tzutalin/labelImg

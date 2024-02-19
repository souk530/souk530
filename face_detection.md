firstprogramまで終了している人
ターミナルに
```
pip install deepfacce
pip install opencv-python

```
を入力し，実行する．
ログがでるので，インストール終了を待つ．

workspaceのディレクトリを作成したうえで以下のディレクトリ構造にする．
```
workspace/
│
├── data/               # 01の人を02から見つける感じ
│   ├── img01.png/
│   └── img02.png/
│
└── face_detection.py/                # ソースコード
```


```
from deepface import DeepFace
import cv2


# result = DeepFace.verify(img1_path = "./data/img01.png", img2_path = "./data/img02.png")
result = DeepFace.verify(img1_path="./data/img01.png", model_name="ArcFace", img2_path="./data/img02.png", detector_backend='ssd')
print(result)


# 画像ファイルのパス
img1_path = './data/img01.png'
img2_path = './data/img02.png'

bbox1 = result['facial_areas']['img1']
bbox2 = result['facial_areas']['img2']
# 画像1にバウンディングボックスを描く
img1 = cv2.imread(img1_path)
cv2.rectangle(img1, (bbox1['x'], bbox1['y']), (bbox1['x']+bbox1['w'], bbox1['y']+bbox1['h']), (0, 255, 0), 2)

# 画像2にバウンディングボックスを描く
img2 = cv2.imread(img2_path)
cv2.rectangle(img2, (bbox2['x'], bbox2['y']), (bbox2['x']+bbox2['w'], bbox2['y']+bbox2['h']), (0, 255, 0), 2)

# 変更を保存
cv2.imwrite('./data/img01_bbox.png', img1)
cv2.imwrite('./data/img02_bbox.png', img2)
```
これをコピペしてpythonファイルを作成．ファイル名は**face_detection.py**とかにしておく．


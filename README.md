# small_tools_for_cv
## 1.改变png格式到numpy格式

import os
from PIL import Image
import numpy as np

dir_root = '/Users/ligang/Desktop/FUTURE_chairs/parts/'
folders = os.listdir(dir_root)

for folder in folders:
    if folder.endswith('_json'):
        files = os.listdir(dir_root+folder)
        for file in files:
            if file=='label.png':
                img_path=dir_root+folder+'/'+file
                a = Image.open(img_path)
                img_np = np.array(a)
                for i in range(len(img_np)):
                    for j in range(len(img_np[0])):
                        if img_np[i][j]!=0:
                            img_np[i][j]=img_np[i][j]+1
                print(np.sum(img_np==2))
                if not os.path.exists('/Users/ligang/Desktop/FUTURE_chairs/mask_numpy/'+folder.split('_json')[0]+'.npy'):
                    np.save('/Users/ligang/Desktop/FUTURE_chairs/mask_numpy/'+folder.split('_json')[0]+'.npy',img_np)
                    print(folder)

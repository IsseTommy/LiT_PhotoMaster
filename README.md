# フォトマスター
***
## １、押さえておくポイント、Swift言語特性
### 写真を取得する方法
1. swiftが用意している補助ツールを入れる。  
初めの行を以下のように変更する。

```
class ViewController: UIViewController, UINavigationControllerDelegate, UIImagePickerControllerDelegate {
```

1. 以下のメゾットを作り、ボタンが押された時などに呼び出す。 

```
func presentPickerController(sourceType: UIImagePickerController.SourceType) {
        if UIImagePickerController.isSourceTypeAvailable(sourceType) {
            let picker = UIImagePickerController()
            picker.sourceType = sourceType
            picker.delegate = self
            self.present(picker, animated: true, completion: nil)
        }
    }
    
    func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [UIImagePickerController.InfoKey: Any]) {
        self.dismiss(animated: true, completion: nil)
        photoImageView.image = info[.originalImage] as? UIImage
    }
```

1. ユーザーにカメラを使うことやアルバムから写真を読み込むことを伝える
1. info.plistでAdd new rowを押し、左側の列にPrivacy設定をしていく。

---

### 共有画面の作り方
以下のようなコードを入力する  
```
if photoImageView.image != nil {
            let activityVC = UIActivityViewController(activityItems: [photoImageView.image!, "#PhotoMaster"], applicationActivities: nil)
            self.present(activityVC, animated: true, completion: nil)
        } else {
            print("画像がありません")
        }
```
まず、photoImageViewに写真があるか確認し、写真がある場合は写真を共有する画面を表示している。

___

## ２、エラー

### ボタンが動作しない
関連付けさせるボタンが多いため全て関連付けされているか確認する。

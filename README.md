# AppleFrameworkWithModal
- UICollectionViewDiffableDataSource
- NSDiffableDataSourceSnapshot
- UICollectionViewCompositionalLayout
- SafariServices

## 🍎 작동 화면

| 작동 화면 |
|:-:|
| ![](https://i.imgur.com/7BjSLFI.gif) |


## 🍎 기존 AppleFrameworkWithCompositionalLayout에 추가된점
```swift
extension FrameworkViewController: UICollectionViewDelegate {
    func collectionView(_ collectionView: UICollectionView, didSelectItemAt indexPath: IndexPath) {
        let framework = frameworkList[indexPath.item]
        print(">>> selected: \(framework.name)")
        
        let storyboard = UIStoryboard(name: "Detail", bundle: nil)
        let vc = storyboard.instantiateViewController(withIdentifier: "FrameworkDetailViewController") as! FrameworkDetailViewController
        vc.selectedApp = framework
        present(vc, animated: true)
    }
}
```
- 기존 프로젝트에서 아이템을 클릭했을 때 새로운 VC(DetailVC)를 띄우는 기능 및 해당 VC 내부 구현 추가.
- 먼저 아이템을 클릭했을떄 특정 작업이 수행되도록 UICollectionViewDelegate 프로토콜을 채택 후 **didSelectItemAt** 메서드를 구현.
- 아이템이 클릭되었을 때 어떤 아이템이 클릭되었는지 테스트.
- "Detail"이라는 새로운 스토리보드를 만들고 해당 스토리보드 안에 아이템을 클릭하면 나올 화면을 구현.
- ![](https://i.imgur.com/RrRqyx0.png)
- 아래 코드를 통해 Detail이라는 이름을 가진 스토리보드를 가져온다. 
```swift
let storyboard = UIStoryboard(name: "Detail", bundle: nil)
```
- 이제 해당 스토리보드에 "FrameworkDetailViewController"라는 이름을 가진 VC를 가져온다.
```swift
let vc = storyboard.instantiateViewController(withIdentifier: "FrameworkDetailViewController") as! FrameworkDetailViewController
```
- 보여질 화면에 뿌려질 데이터가 필요함으로써 FrameworkDetailViewController의 selectedApp 프로퍼티에 넘겨준다.
```swift
vc.selectedApp = framework
```
- 화면을 모달로 띄워준다.
```swift
present(vc, animated: true)
```

## 🍎 Learn More 버튼을 클릭해 사파리 띄우기
![](https://i.imgur.com/6JKfjZ9.png)
```swift
@IBAction func learnMoreButtonTapped(_ sender: UIButton) {
    guard let url = URL(string: selectedApp.urlString) else { return}
    let safari = SFSafariViewController(url: url)
    present(safari, animated: true)
}
```
- 이전 VC에서 현재 VC를 띄우기 전에 'vc.selectedApp = framework' 코드로 넘겨주었던 데이터를 사용해 URL을 만들어준다.
```swift
guard let url = URL(string: selectedApp.urlString) else { return }
```
- 만들어진 url로 사파리를 띄운다
```swift
let safari = SFSafariViewController(url: url)
present(safari, animated: true)
```

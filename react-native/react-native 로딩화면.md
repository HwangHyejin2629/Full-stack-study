# 로딩화면
- npm install expo-splash-screen --force
- assets 폴더에 아이콘으로 사용할 1024x1024크기의 이미지를 icon.png로, 로딩화면에 사용할 1242x2436크기의 이미지를 splash.png파일로 교체해 넣는다.
- SplashScreen.preventAutoHideAsync() : 스플래시 화면이 자동으로 숨겨지지 않도록 설정하여 초기화 작업이 완료될 때까지 유지함
- prefetch() : 원격 URL의 이미지를 캐싱하기 위해 사용
- fromModule()
```js
import * as SplashScreen from 'expo-splash-screen';
import { Asset } from 'expo-asset';

SplashScreen.preventAutoHideAsync();

const cacheImages = images => {
    return images.map(image => {
        if (typeof image === 'string') {
            return Image.prefetch(image); //URL로 제공된 이미지의 경우, Image.prefetch로 캐싱
        } else {
            return Asset.fromModule(image).downloadAsync();//로컬파일인 경우, expo-asset에서 제공하는 다운로드 방식으로 캐싱
        }
    })
}
```
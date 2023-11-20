# Three.js - Textures

Texture là một hình ảnh hoặc màu sắc được thêm vào vật thể để tạo ra một hiệu ứng thực tế hơn. Đây là một yếu tố quan trọng của Three.js.


## Cách sử dụng texture

Đầu tiên, sử dùng đối tượng `TextureLoader()` để tải texture từ một hình ảnh. Đối tượng này có một hàm con `load()` để tải ảnh từ đường dẫn của ảnh.

```js
const loader = new THREE.TextureLoader()
texture.load('/path/to/the/image')
```

Sau khi tải xong, ta có thể sử dụng texture này cho vật thể bằng cách truyền vào thuộc tính `map` của vật thể.

```js
const geometry = new THREE.PlaneGeometry(planeSize, planeSize)
const material = new THREE.MeshPhongMaterial({
    map: texture,
    side: THREE.DoubleSide
})
const board = new THREE.Mesh(geometry, material)
```

Trong ví dụ trên, ta đã áp dụng texture cho plane. Tuy nhiên, ta có thể áp dụng texture cho bất kỳ vật thể nào trong Three.js.

Texture có các tùy chỉnh cho việc lặp hình, thay đổi vị trí, và xoay. Mặc định, các texture trong Three.js không lặp lại. Đối tượng texture có 2 thuộc tính `wrapS` để lặp theo chiều ngang và `wrapT` để lặp theo chiều dọc.

Thuộc tính `magFilter` để thay đổi kích thước của texture khi phóng to. Giá trị `THREE.NearestFilter` sẽ dùng màu của pixel gần nhất. Giá trị `THREE.LinearFilter` sẽ dùng màu của 4 pixel xung quanh để tính toán giá trị màu chính xác.

```js
texture.wrapS = THREE.RepeatWrapping
texture.wrapT = THREE.RepeatWrapping
texture.magFilter = THREE.NearestFilter
```

Ngoài ra cũng có thể cài đặt số lần lặp của texture bằng cách sử dụng thuộc tính `repeat` của texture. Giá trị của thuộc tính này là một đối tượng có 2 thuộc tính `x` và `y` để chỉ số lần lặp theo chiều ngang và chiều dọc.

```js
const timesToRepeatHorizontally = 4
const timesToRepeatVertically = 2
texture.repeat.set(timesToRepeatHorizontally, timesToRepeatVertically)
```

## Texture Mapping

### Base Color Map

Base Color Map là hình ảnh cơ bản vẽ lên màu sắc cho bề mặt.

```js
const textureMap = new THREE.TextureLoader().load('/path/to/texture-map')
material.map = textureMap
```

Để vẽ thêm chiều sau cho vật thể, ta cần sử dụng Bump Map, Normal Map hoặc Dispalcement Map.

### Bump Map

Bump Map là một hình ảnh đen trắng, độ đậm nhạt của mỗi pixel sẽ quyết định chiều cao trên bề mặt vật thể.

```js
const textureBumpMap = new THREE.TextureLoader().load('/path/to/bump-map')
material.bumpMap = textureBumpMap
```

### Normal Map

Normal Map mô tả vector của mỗi pixel, vector này sẽ được sử dụng để tính toán cách ánh sáng ảnh hưởng đến chất liệu sử dụng trên vật thể. Nó tạo ra ảo giác về chiều sâu trên vật thể phẳng.

```js
const textureNormalMap = new THREE.TextureLoader().load('/path/to/normal-map')
material.normalMap = textureNormalMap
```

### Displacement Map

Nếu Normal Map tạo ra ảo giác về chiều sâu, thì Displacement Map sẽ thay đổi thực sự chiều cao của vật thể dựa trên texture.

```js
const textureDisplacementMap = new THREE.TextureLoader().load('/path/to/displacement-map')
material.displacementMap = textureDisplacementMap
```

### Roughness Map

Roughness Map mô tả độ nhám của vật thể. Giá trị của mỗi pixel sẽ quyết định cách vật thể phản chiếu ánh sáng trên bề mặt.

```js
const textureRoughnessMap = new THREE.TextureLoader().load('/path/to/roughness-map')
material.roughnessMap = textureRoughnessMap
```

### Ambient Occlusion Map

Ambient Occlusion Map nhấn mạnh vào các khu vực bị che khuất trên vật thể. Nếu so sánh vật thể khi sử dụng Roughness Map và Ambient Oclustion Map, ta sẽ thấy rằng vật thể khi sử dụng Ambient Occlusion Map sẽ có các khu vực bóng có độ tương phản cao hơn.

```js
const textureAmbientOcclusionMap = new THREE.TextureLoader().load('/path/to/AmbientOcclusion-map')
material.aoMap = textureAmbientOcclusionMap
// second UV
mesh.geometry.attributes.uv2 = mesh.geometry.attributes.uv
```

### Metalness Map

Metalness Map mô tả độ giống với kim loại của vật thể.

```js
const textureMetalnessMap = new THREE.TextureLoader().load('/path/to/metalness-map')
material.metalnessMap = textureMetalnessMap
```

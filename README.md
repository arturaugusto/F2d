# F2d

```javascript
const arr = [0,0,0,0, 0,1,1,0, 0,0,0,0, 0,1,1,0, 0,0,0,0, 0,0,0,0];

const intoChunks = (arr, sizes) => {
  return arr.reduce((a, c, i) => {
    if (!(i % sizes)) a.push([])
    a[a.length-1].push(c)
    return a
  }, [])
}

const chunks = intoChunks(arr, 4)
//[[0,0,0,0],[0,1,1,0],[0,0,0,0],[0,1,1,0],[0,0,0,0],[0,0,0,0]]

const leftTrim = (chunks, threshold) => {
  threshold = threshold === undefined ? 1 : threshold
  for (let i = 0; i < chunks.length; i++) {
    if (chunks.map(x => x[i]).reduce((ax, cx) => ax+cx, 0) >= threshold) {
      return chunks.map(x => x.slice(i))
    }
  }
  return new Array(chunks.length).fill().map(x => [])
}

const leftTrimmed = leftTrim(chunks)
//[[0,0,0],[1,1,0],[0,0,0],[1,1,0],[0,0,0],[0,0,0]]

const rightTrim = (chunks, threshold) => {
  threshold = threshold === undefined ? 1 : threshold
  for (let i = chunks.length - 1; i >= 0; i--) {
    if (chunks.map(x => x[i]).reduce((ax, cx) => ax+cx, 0) >= threshold ) {
      return chunks.map(x => x.slice(0, i+1))
    }
  }
  return new Array(chunks.length).fill().map(x => [])
}

const leftRightTrimmed = rightTrim(leftTrimmed)
// [[0,0],[1,1],[0,0],[1,1],[0,0],[0,0]]


const topTrim = (chunks, threshold) => {
  threshold = threshold === undefined ? 1 : threshold
  for (let i = 0; i < chunks.length; i++) {
    if (chunks[i].reduce((ax, cx) => ax+cx, 0) >= threshold) {
      return chunks.slice(i)
    }
  }
  return []
}

const leftRightTopTrimmed = topTrim(leftRightTrimmed)
// [[1,1],[0,0],[1,1],[0,0],[0,0]]

const bottomTrim = (chunks, threshold) => {
  threshold = threshold === undefined ? 1 : threshold
  for (let i = chunks.length - 1; i >= 0; i--) {
    if (chunks[i].reduce((ax, cx) => ax+cx, 0) >= threshold) {
      return chunks.slice(0, i+1)
    }
  }
  return []
}

const leftRightTopBottomTrimmed = bottomTrim(leftRightTopTrimmed)
// [[1,1],[0,0],[1,1]]

const slice2d = (chunks, y0, y1, x0, x1) => {
  return chunks.slice(y0, y1).map(row => row.slice(x0, x1))
}

const slice = slice2d(chunks, 3, 5, 1, 3)
// [[1,1],[0,0]]

```

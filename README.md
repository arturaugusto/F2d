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

const leftTrim = (chunks) => {
  for (let i = 0; i < chunks.length; i++) {
    if (chunks.map(x => x[i]).reduce((ax, cx) => ax+cx, 0)) {
      return chunks.map(x => x.slice(i))
    }
  }
  return new Array(chunks.length).fill().map(x => [])
}

const leftTrimmed = leftTrim(chunks)
//[[0,0,0],[1,1,0],[0,0,0],[1,1,0],[0,0,0],[0,0,0]]

const rightTrim = (chunks) => {
  for (let i = chunks.length - 1; i >= 0; i--) {
    if (chunks.map(x => x[i]).reduce((ax, cx) => ax+cx, 0)) {
      return chunks.map(x => x.slice(0, i+1))
    }
  }
  return new Array(chunks.length).fill().map(x => [])
}

const leftRightTrimmed = rightTrim(leftTrimmed)
// [[0,0],[1,1],[0,0],[1,1],[0,0],[0,0]]


const topTrim = (chunks) => {
  for (let i = 0; i < chunks.length; i++) {
    if (chunks[i].reduce((ax, cx) => ax+cx, 0)) {
      return chunks.slice(i)
    }
  }
  return []
}

const leftRightTopTrimmed = topTrim(leftRightTrimmed)
// [[1,1],[0,0],[1,1],[0,0],[0,0]]

const bottomTrim = (chunks) => {
  for (let i = chunks.length - 1; i >= 0; i--) {
    if (chunks[i].reduce((ax, cx) => ax+cx, 0)) {
      return chunks.slice(0, i+1)
    }
  }
  return []
}

const leftRightTopBottomTrimmed = bottomTrim(leftRightTopTrimmed)
// [[1,1],[0,0],[1,1]]





```

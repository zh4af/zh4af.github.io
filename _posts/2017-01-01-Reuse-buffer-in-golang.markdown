---
layout: post
title:  "Reuse buffer in golang"
date:   2017-01-01 12:00:00
categories: jekyll update
---

Reuse buffer in using many small memory obj:

{% highlight golang %}
func newBufferPool() *bufferPool {
	return &bufferPool{
		&sync.Pool{New: func() interface{} {
			return bytes.NewBuffer(make([]byte, 0, 1))
		}},
	}
}

func (bp *bufferPool) Get() *bytes.Buffer {
	return (bp.Pool.Get()).(*bytes.Buffer)
}

func (bp *bufferPool) Put(b *bytes.Buffer) {
	b.Truncate(0)
	bp.Pool.Put(b)
}
{% endhighlight %}

[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]:    http://jekyllrb.com

<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>yby的数理方法简记1</title>

    <script src="https://cdn.tailwindcss.com"></script>

    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet" />

    <script>
      window.MathJax = {
        tex: {
          inlineMath: [['$', '$'], ['\\(', '\\)']],
          displayMath: [['$$', '$$'], ['\\[', '\\]']],
          processEscapes: true
        },
        options: {
          skipHtmlTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code']
        }
      };
    </script>
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>

    <style>
      body { 
        font-family: 'Inter', sans-serif; 
        background-color: #f8f9fa; 
        font-size: 160%; /* Drastically increase base font size */
      }
      .container { max-width: 1000px; } /* Expand max-width for better content flow */
      .handwritten {
        font-family: 'Segoe Script', 'Comic Sans MS', cursive;
        background-color: #fff;
        padding: 4rem; /* Increase padding */
        border-radius: 1.5rem; /* Larger border-radius */
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15); /* More prominent shadow */
      }
      .note-image {
        max-width: 100%;
        height: auto;
        border-radius: 0.75rem; /* Larger border-radius for images */
      }
      .note-image-right {
        max-width: 350px; /* Adjust size */
        float: right;
        margin-left: 2.5rem;
        margin-bottom: 2.5rem;
      }
      .note-image-left {
        max-width: 350px; /* Adjust size */
        float: left;
        margin-right: 2.5rem;
        margin-bottom: 2.5rem;
      }
      .note-image-center {
        max-width: 500px; /* Adjust size */
        display: block;
        margin: 2.5rem auto;
      }
      .small-text { 
        font-size: 1.15em; /* Make small text even larger */
        color: #444; 
        line-height: 2.2; /* Increase line height */
        margin: 1.5rem 0; /* Adjust margin */
      }
      .small-text mjx-container { font-size: 1.25em !important; } /* Ensure formulas in small text are also larger */

      .block { margin-bottom: 2.5rem; } /* Increase spacing between blocks */
      .clear { clear: both; }

      h1 { font-size: 3.5rem; } /* Adjust heading sizes */
      h2 { font-size: 3rem; }
      h3 { font-size: 2.5rem; }
      p { line-height: 2.2; margin-bottom: 2.5rem; } /* Adjust paragraph spacing */
      li { line-height: 2.2; margin-bottom: 2rem; }
    </style>
</head>
<body class="p-16">
  <div class="container mx-auto handwritten">
    <h1 class="font-bold text-center mb-12">笔记整理1</h1>
    <p class="text-center text-gray-500 mb-14">yby</p>

    <nav class="mb-16 p-12 bg-gray-100 rounded-xl shadow-inner">
      <h2 class="font-bold mb-10">目录</h2>
      <ul class="space-y-8 text-gray-700">
        <li><a href="#section1" class="hover:text-blue-600 transition-colors duration-200">1. 小圆弧定理</a></li>
        <li><a href="#section2" class="hover:text-blue-600 transition-colors duration-200">2. 柯西公式的推导</a></li>
        <li><a href="#section3" class="hover:text-blue-600 transition-colors duration-200">3. 推广到高阶导数</a></li>
        <li><a href="#section4" class="hover:text-blue-600 transition-colors duration-200">4. 泰勒定理的证明</a></li>
        <li><a href="#section5" class="hover:text-blue-600 transition-colors duration-200">5. 洛朗展开</a></li>
      </ul>
    </nav>
    <hr class="my-14 border-gray-300" />

    <section id="section1" class="mb-16 p-12 bg-gray-50 rounded-xl">
      <h2 class="font-semibold mb-10">1. 小圆弧定理</h2>

      <div class="block">
        <img src="https://mmbiz.qpic.cn/mmbiz_jpg/n1DeXGK5z8cOpXkRm04NWfQB7NVoZDVZvBe9Vdg8ljhTU9Ria0nSvEfxFicq4g2IQAgCoqRyib37y8rwj6Ijnotvw/0?wxfrom=12&wx_fmt=jpg&tp=wxpic&usePicPrefetch=1" alt="" class="note-image note-image-right" />
        <div>
          <p class="mb-10">
            若函数 $f(z)$ 在 $z_0$ 的无心邻域内连续，并且在小圆弧 $C_r$ 上一致成立：
          </p>
          <p class="mb-10">$$\lim_{z \to z_0} (z - z_0) f(z) = k$$</p>
        </div>
      </div>

      <p class="small-text">
        “一致成立”指与路径无关；如果以不同路径趋于 $z_0$ 时取值不同，则极限不存在。
      </p>

      <div class="block">
        <p class="mb-8">则有小圆弧定理：</p>
        <p>$$\lim_{r \to 0} \int_{C_r} \varphi(z)\,dz = i k (\theta_2 - \theta_1)$$</p>
      </div>
      <div class="block">
        <h3 class="font-semibold mb-8">小圆弧定理的证明</h3>
        <p class="mb-8">
          根据极限定义，对于任意 $\epsilon > 0$，存在 $\delta > 0$，使得当 $|z-z_0| < \delta$ 时，有 $|(z-z_0)\varphi(z) - k| < \epsilon$。
        </p>
        <p class="mb-8">
          我们的目标是证明 $\lim_{r \to 0} \left| \int_{C_r} \varphi(z) dz - ik(\theta_2 - \theta_1) \right| = 0$。
          由于 $\int_{C_r} \frac{dz}{z-z_0} = i(\theta_2-\theta_1)$，我们有：
        </p>
        <p>
          $$\left| \int_{C_r} \varphi(z) dz - k \int_{C_r} \frac{dz}{z-z_0} \right| = \left| \int_{C_r} \left( \varphi(z) - \frac{k}{z-z_0} \right) dz \right|$$
        </p>
        <p>
          由积分的三角不等式和ML不等式，当 $r < \delta$ 时：
        </p>
        <p>
          $$\le \int_{C_r} \left| \varphi(z) - \frac{k}{z-z_0} \right| |dz|$$
        </p>
        <p>
          $$= \int_{C_r} \left| \frac{(z-z_0)\varphi(z) - k}{z-z_0} \right| |dz|$$
        </p>
        <p>
          $$= \int_{C_r} \frac{|(z-z_0)\varphi(z) - k|}{|z-z_0|} |dz|$$
        </p>
        <p>
          $$\le \int_{C_r} \frac{\epsilon}{r} |dz| = \frac{\epsilon}{r} \int_{C_r} |dz| = \frac{\epsilon}{r} \cdot r(\theta_2 - \theta_1) = \epsilon (\theta_2 - \theta_1)$$
        </p>
        <p>
          由于 $\epsilon$ 是任意小的正数，且 $(\theta_2 - \theta_1)$ 是常数，所以当 $r \to 0$ 时，该式趋于0。因此，原式成立。
        </p>
      </div>
      <p class="text-gray-600 mb-12 mt-14"><strong>前置条件：</strong></p>
      <ol class="list-decimal list-inside pl-10 text-gray-600">
        <li class="mb-8">
          极限的定义：
          <div class="small-text">
            设 $w = f(z)$ 是在 $z_0$ 的无心邻域中定义的单值函数，若任给 $\epsilon > 0$，存在 $\delta > 0$，当 $|z - z_0| < \delta$ 时，有 $|f(z) - w_0| < \epsilon$，则称 $\lim_{z\to z_0} f(z) = w_0$。
          </div>
        </li>
        <li>
          $\displaystyle \int_{C_r} \frac{dz}{z-\alpha} = i(\theta_2-\theta_1)$ 的推导：
          <div class="block">
            <img src="https://mmbiz.qpic.cn/mmbiz_jpg/n1DeXGK5z8cOpXkRm04NWfQB7NVoZDVZaQZQCHV3po5S7AdLNGu6xAlZLHOicrqRm5icfnYYgBRia1ecQj5J1kVqg/0?wxfrom=12&wx_fmt=jpg&tp=wxpic" alt="" class="note-image note-image-left" />
            <div class="small-text">
              积分回路是以 $\alpha$ 为圆心的圆弧 $C_r: z-\alpha = r e^{i\theta}$，其中 $\theta_1 \le \theta \le \theta_2$。
              由参数化 $z-\alpha = r e^{i\theta}$ 得 $dz = i r e^{i\theta} d\theta$。因此
              $$\int_{C_r} \frac{dz}{z-\alpha} = \int_{\theta_1}^{\theta_2} \frac{i r e^{i\theta}}{r e^{i\theta}}\, d\theta = \int_{\theta_1}^{\theta_2} i\, d\theta = i (\theta_2 - \theta_1).$$
            </div>
          </div>
        </li>
      </ol>
      <div class="clear"></div>
    </section>

    <section id="section2" class="mb-16 p-12 bg-gray-50 rounded-xl">
      <h2 class="font-semibold mb-10">2. 柯西公式的推导</h2>

      <img src="https://mmbiz.qpic.cn/mmbiz_jpg/n1DeXGK5z8cOpXkRm04NWfQB7NVoZDVZuibQTjWPdWLlpzsicOud1qicBzBPBm6RkfaaibbS7r8sbbSqkIJ2jtQWdg/0?wxfrom=12&wx_fmt=jpg&tp=wxpic" alt="" class="note-image note-image-right" />
      <p class="mb-10">
        根据小圆弧定理，若函数 $f(z)$ 在区域 $L$ 内解析，且 $a$ 为 $L$ 的内点，则可构造函数 $\varphi(z) = \dfrac{f(z)}{z-a}$。
      </p>
      <p class="mb-10">此时
        $$k = \lim_{z \to a} (z-a)\, \varphi(z) = \lim_{z \to a} (z-a)\,\frac{f(z)}{z-a} = f(a).$$
      </p>
      <p class="mb-10">
        当 $\theta_2 - \theta_1 = 2\pi$ 时，可得到柯西公式：
      </p>
      <p class="mb-10">$$f(a) = \frac{1}{2\pi i} \oint_{L} \frac{f(z)}{z-a}\, dz$$</p>
      <p class="mb-10">
        将 $a$ 和 $z$ 代换，就得到了我们熟悉的柯西公式：
      </p>
      <p class="mb-10">$$f(z) = \frac{1}{2\pi i} \oint_{L} \frac{f(\zeta)}{\zeta - z}\, d\zeta$$</p>

      <img src="https://mmbiz.qpic.cn/mmbiz_jpg/n1DeXGK5z8cOpXkRm04NWfQB7NVoZDVZqIUZOn7hwsg17lpwbaO6CWqicgANIBGAWib4ptXTaSWqOibZo9GHDur5g/0?wxfrom=12&wx_fmt=jpg&tp=wxpic" alt="" class="note-image note-image-center" />
      <p class="mb-10 text-gray-600">
        <strong>推广到多连通区域：</strong>
        </p>
        <p class="small-text">
          做小割线变成单通区域，不难看出同样成立。
        </p>
        <p>
        $$\oint_{L} = \oint_{L_1} + \oint_{L_2} + \dots + \oint_{L_k} + \oint_{L_0}$$
      </p>
      <p class="small-text">来回的割线抵消了。</p>
      <div class="clear"></div>
    </section>

    <section id="section3" class="mb-16 p-12 bg-gray-50 rounded-xl">
      <h2 class="font-semibold mb-10">3. 推广到高阶导数</h2>

      <div class="block">
        <p class="mb-10">将柯西公式代入导数定义：</p>
        <p>$$f'(z) = \lim_{\Delta z \to 0} \frac{f(z+\Delta z) - f(z)}{\Delta z}$$</p>
        <p>$$= \frac{1}{2\pi i} \lim_{\Delta z \to 0} \frac{1}{\Delta z}\!\left[ \oint_{L} \frac{f(\xi)}{\xi - (z+\Delta z)}\, d\xi - \oint_{L} \frac{f(\xi)}{\xi - z}\, d\xi \right]$$</p>
        <p>$$= \frac{1}{2\pi i} \lim_{\Delta z \to 0} \oint_{L} f(\xi) \frac{(\xi-z) - (\xi - (z+\Delta z))}{\Delta z\,[\xi-(z+\Delta z)](\xi - z)}\, d\xi$$</p>
        <p>$$= \frac{1}{2\pi i} \lim_{\Delta z \to 0} \oint_{L} \frac{f(\xi)}{[\xi-(z+\Delta z)](\xi - z)}\, d\xi.$$</p>
      </div>
      <div class="block">
        <p class="mb-10">交换极限与积分的顺序，得：</p>
        <p>$$f'(z) = \frac{1}{2\pi i} \oint_{L} \frac{f(\xi)}{(\xi - z)^2}\, d\xi.$$</p>
      </div>
      <div class="block">
        <p class="mb-10">反复使用定义，并用数学归纳法可得复变函数的高阶导数公式：</p>
        <p>$$f^{(n)}(z) = \frac{n!}{2\pi i} \oint_{L} \frac{f(\xi)}{(\xi - z)^{n+1}}\, d\xi.$$</p>
      </div>
    </section>

    <section id="section4" class="mb-16 p-12 bg-gray-50 rounded-xl">
      <h2 class="font-semibold mb-10">4. 泰勒定理的证明</h2>

      <img src="https://mmbiz.qpic.cn/mmbiz_jpg/n1DeXGK5z8cOpXkRm04NWfQB7NVoZDVZkerZglMR1lSAH6RsslKOibWDC82k2MVVUoxapySsZL338pFRhFfTO7w/0?wxfrom=12&wx_fmt=jpg&tp=wxpic" alt="" class="note-image note-image-left" />
      <p class="mb-10">已知柯西公式：</p>
      <p>$$f(z) = \frac{1}{2\pi i} \oint_{C} \frac{f(\xi)}{\xi - z}\, d\xi$$</p>
      <p class="small-text">在圆域 $|z-b| < R$ 内解析。$\xi$ 在 $C_R$ 上，不一定解析。以 $b$ 为圆心作一圆 $C_\rho$，取 $z$ 为 $C_\rho$ 上的点。</p>
      <p class="mb-10">利用等比级数 $\dfrac{1}{1-t} = \sum_{k=0}^{\infty} t^k$，将 $\dfrac{1}{\xi - z}$ 展开为级数：</p>
      <p>$$\frac{1}{\xi - z} = \frac{1}{(\xi - b) - (z - b)} = \frac{1}{\xi - b}\, \frac{1}{1 - \dfrac{z - b}{\xi - b}} = \sum_{k=0}^{\infty} \frac{(z - b)^k}{(\xi - b)^{k+1}}.$$</p>
      <p class="mb-10">代入柯西公式：</p>
      <p>$$f(z) = \frac{1}{2\pi i} \oint_{C} f(\xi) \sum_{k=0}^{\infty} \frac{(z - b)^k}{(\xi - b)^{k+1}}\, d\xi$$</p>
      <p class="small-text">接下来交换积分和求和顺序。严格证明需验证一致收敛；此处从略。</p>
      <p>$$f(z) = \sum_{k=0}^{\infty} \frac{1}{2\pi i} (z - b)^k \oint_{C} \frac{f(\xi)}{(\xi - b)^{k+1}}\, d\xi$$</p>
      <p class="mb-10">结合高阶导数公式，可得泰勒定理：</p>
      <p>$$f(z) = \sum_{k=0}^{\infty} \frac{f^{(k)}(b)}{k!} (z - b)^k.$$</p>
      <div class="clear"></div>
    </section>

    <section id="section5" class="p-12 bg-gray-50 rounded-xl">
      <h2 class="font-semibold mb-10">5. 洛朗展开</h2>

      <img src="https://mmbiz.qpic.cn/mmbiz_jpg/n1DeXGK5z8cOpXkRm04NWfQB7NVoZDVZaQZQCHV3po5S7AdLNGu6xAlZLHOicrqRm5icfnYYgBRia1ecQj5J1kVqg/0?wxfrom=12&wx_fmt=jpg&tp=wxpic" alt="" class="note-image note-image-left" />
      <p class="mb-10">泰勒定理是将圆域中的解析函数展开为幂级数，洛朗定理可仿照此法推广到环形区域。</p>
      <p class="mb-10">
        若函数 $f(z)$ 在环域 $R_2 < |z-b| < R_1$ 内解析，根据推广的柯西公式：
      </p>
      <p>$$f(z) = \frac{1}{2\pi i} \oint_{C_1} \frac{f(\xi)}{\xi - z}\, d\xi + \frac{1}{2\pi i} \oint_{C_2} \frac{f(\xi)}{\xi - z}\, d\xi$$</p>
      <p>
        对于第一项 $I_1 = \frac{1}{2\pi i} \oint_{C_1} \frac{f(\xi)}{\xi - z}\, d\xi$，仿照泰勒定理的证明，我们得到：
      </p>
      <p>$$I_1 = \sum_{k=0}^{\infty} \frac{1}{2\pi i} \oint_{C_1} \frac{f(\xi)}{(\xi - b)^{k+1}}\, d\xi (z-b)^k$$</p>
      <p>
        对于第二项 $I_2 = \frac{1}{2\pi i} \oint_{C_2} \frac{f(\xi)}{\xi - z}\, d\xi$，我们对 $\frac{1}{\xi - z}$ 进行展开：
      </p>
      <p>$$\frac{1}{\xi - z} = -\frac{1}{z - \xi} = -\frac{1}{(z - b) - (\xi - b)} = -\frac{1}{z - b} \frac{1}{1 - \frac{\xi - b}{z - b}} = -\sum_{k=0}^{\infty} \frac{(\xi-b)^k}{(z-b)^{k+1}}$$</p>
      <p>
        代入 $I_2$ 并交换积分和求和顺序，得到：
      </p>
      <p>$$I_2 = -\frac{1}{2\pi i} \oint_{C_2} f(\xi) \sum_{k=0}^{\infty} \frac{(\xi-b)^k}{(z-b)^{k+1}}\, d\xi = \sum_{k=0}^{\infty} \left[ -\frac{1}{2\pi i} \oint_{C_2} \frac{f(\xi)}{(\xi-b)^{-k}}\, d\xi \right] (z-b)^{-k-1}$$</p>
      <p>
        令 $n = -k-1$，则当 $k=0$ 时，$n=-1$；当 $k \to \infty$ 时，$n \to -\infty$。
      </p>
      <p>$$I_2 = \sum_{n=-1}^{-\infty} \left[ \frac{1}{2\pi i} \oint_{C_2} \frac{f(\xi)}{(\xi-b)^{n+1}}\, d\xi \right] (z-b)^n$$</p>
      <p>
        将 $I_1$ 和 $I_2$ 相加，并令系数 $a_n = \frac{1}{2\pi i} \oint_{C} \frac{f(\xi)}{(\xi-b)^{n+1}}\, d\xi$，最终得到洛朗展开式：
      </p>
      <p>$$f(z) = \sum_{n=-\infty}^{\infty} a_n (z-b)^n$$</p>
      <p class="small-text mt-12">
       个人理解：
        把外面当无限大的圆，把外面当里面？那也在内部了。
      </p>
      <div class="clear"></div>
    </section>
  </div>
</body>
</html>

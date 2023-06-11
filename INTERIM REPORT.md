
![External Image|sban cover hs-med](iiitlogo.jpeg)
# Image Compression Interim Report
### Project Submission Date: 20-06-2023
------------
## By:-
- ### Ashwin Rudraraju, 2022101022
- ### Dikshant, 202210238
- ### Srivarshitha Medarametla, 2022102030
--------------------------
## Overview Of the Final Report:
In the final Project report, we'll be covering the following topics:
- ###### Motivation 
	- History of Image compression. 
	- Need of Image Compression.
	- Benefits.
- ###### JPEG Technique of image compression
	- we will be explaining the JPEG Image compression.
	- How SVD & Bias are used in JPEG compression.
	- We will try and illustrate image compression through a program (hopefully it'll be a python program).
- ###### WEBP
	- we will be briefly explaining "webp" which is google's new image compression technique (which can be considered as State Of Art Technique in the field of Image Compression.)
- ###### Linear Algebra Topics Used
	- SVD,
	- Concepts of Basis,
	- Orthogonality, etc.
- ###### Conclusion
## Distribution of Work
- Ashwin Rudraraju - DCT in JPEG, WEBP& Writing Slides.
- Dikshant - Motivation & JPEG (Except DCT) & Writing The Latex Doc.
- Srivarshitha Medarametla- Writing Code and Animations part.
## Timeline
#DAY1 : Distribution of work
#DAY2: Researched for Resources and Started making some slides for final evaluation.
#DAY3: Prepared Notes About important things in JPEG and  it's functioning. Prepared slides                     on webp.
#DAY4/5: Slides on lossy/lossless form of compression and started animation and coding part.
#DAY6: Prepared PDF for Interim Report.  
- ## Resources Referred:
	- https://en.wikipedia.org/wiki/JPEG
	- Linear Algebra A Modern Introduction [page no. 630]  (by~David Poole) 
	- Image Compression And Linear Algebra              (By~Sunny Verma, J.P. Krishna)
	    (https://www.cmi.ac.in/~ksutar/NLA2013/imagecompression.pdf)
	    
	- Linear Algebra In Image Compression: SVD and DCT (By~Andrew Fraser)
	   (https://www.math.utah.edu/~gustafso/s2019/2270/projects-2019/presented/fraser/Linear%20Algebra%20in%20Image%20Compression_%20SVD%20and%20DCT.pdf)
	   
	- JPEG Image Compression using Singular Value Decomposition (By~ Mrs. Rehna V.J, Mr. Abhranil Dasgupta)
	    (https://www.researchgate.net/publication/351096054_JPEG_Image_Compression_using_Singular_Value_Decomposition)
	- 
           (https://ieeexplore.ieee.org/abstract/document/4426357) 
           (https://www.ijcsmc.com/docs/papers/April2016/V5I4201635.pdf)

-------------------------------

----------
<div style="page-break-after: always;"></div>

## Motivation:
Taking Black and white Picture as example$(\because grey-scale\ has\ only\ two\ values)$  
![[bw_panda.jpeg]]
If we look at the above black and white picture. We will realize that a typical pixel gives us a grey-scale value. 
$\because$ pixel is the value of $X_{i}.$ s.t $X_{i} \in [0,255) \implies 8\ bits$
Then we have that $\forall X \in \mathbb{R}^{n}, where\ n=(512)^{2}$
We can say that pixel is the vector of length $(512)^{2}$ through which image is generated.

If it was a coloured image than we would have length of vector as $3\times (512)^{2}\ (\because$ coloured picture has 3D co-ordinate system of RGB values).
###### "Which will be an enormous amount of info. $\implies$ sending these images would consume a lot of internet/time. Also storing these images would occupy a lot of space in hard-drive."
###### This gives rise to several "Compression Techniques of Images" like png, jpeg.
Since, JPEG being is widely used. So, we'll be discussing about jpeg in our project.

------------------
<div style="page-break-after: always;"></div>

## JPEG(Joint Photographic Experts Group)
- ### HOW??
If we again have a look at this picture
![[panda.jpeg]]
###### What basis do it have??
since standard basis - every pixel given a value.
$\implies$ 
$$
X=
\begin{bmatrix}
 \ .\
 \\
 \ .\
 \\
 \ .\
 \\
 \ .\
 \\
 \ x\ (s.t\ x \in [0,255)
 \\
 \ .\
 \\
 \ .\
 \\
 \ .\
 \\
 \ .\
\end{bmatrix}_{512^{2} \times 1}
$$
so we might have few pixels that are very close for example:
$$
X=
\begin{bmatrix}
 \ .\
 \\
 \ .\
 \\
 \ 73\
 \\
 \ 75\
 \\
 \ .\
 \\
 \ .\

\end{bmatrix}
$$

since 73 and 75 are very close on a grey-scale. And since these pixels are adjacent to each other i.e they are co-related. This gives rise to the possibility of Image Compression. Since if we compress them, we will not be able to identify the difference between the compressed pixels.

###### Second Example:
![[black.jpeg]]

In the above picture all the pixels have same values. $\implies$ image where standard basis is Lossy.
$$ $$
Here, Standard Basis that gives the value of every pixel makes **no use** of the fact that **we are getting a whole lot of pixels who tends to have same grey level.**

###### So, if we keep this in mind and try to make a new standard Basis then it would be the following:
$$
\begin{bmatrix}
 \ 1\
 \\
 \ 0\
 \\
 \ 0\
 \\
 \ .\
 \\
 \ .\
 \\
 \ .\
 \\
 \ 0\

\end{bmatrix}

\begin{bmatrix}
 \ 0\
 \\
 \ 1\
 \\
 \ 0\
 \\
 \ 0\
 \\
 \ .\
 \\
 \ .\
 \\
 \ 0\

\end{bmatrix}
.........
\begin{bmatrix}
 \ 0\
 \\
 \ 0\
 \\
 \ .\
 \\
 \ .\
 \\
 \ .\
 \\
 \ .\
 \\
 \ 1\

\end{bmatrix}
\tag{Eq. 1}
$$
###### Creating a Better Basis
Since we are considering only 1 colour that is solid colour $\implies basis\ could\ just\ be\ matrix\ of\ 1$
$$
\begin{bmatrix}
1 \\
1 \\
1 \\
1 \\
1 \\
1 \\
1 \\
1
\end{bmatrix}
$$

###### Expanding It Further for other types of pictures as well
CASE 2:
![[dot.jpeg]]
Since the image is like black/white pixel image $\implies$ we will use a checkerboard vector
$$
\begin{bmatrix}
1 \\
-1 \\
1 \\
-1 \\
1 \\
-1 \\
1 \\
-1
\end{bmatrix}
$$

CASE 3:
![[bwhlf.png]]
Since half of the image is light and half is dark $\implies$ basis vector will be like
$$
\begin{bmatrix}
1 \\
1 \\
1 \\
1 \\
-1 \\
-1 \\
-1 \\
-1
\end{bmatrix}
$$

Combining CASE 2 and 3 with Second Example
We get the following basis vector:
$$
\begin{bmatrix}
1 \\
1 \\
1 \\
1 \\
1 \\
1 \\
1 \\
1
\end{bmatrix}
\begin{bmatrix}
1 \\
-1 \\
1 \\
-1 \\
1 \\
-1 \\
1 \\
-1
\end{bmatrix}
\begin{bmatrix}
1 \\
1 \\
1 \\
1 \\
-1 \\
-1 \\
-1 \\
-1
\end{bmatrix}
$$
- ### Now the question arises what BASIS to use ???
	- now a days JPEG uses DCT(Discrete Cosine Transformation).
	- But I will be explaining it using Fourier Basis and how to improve it using Wavelet basis.(DWT).
	- since DCT is similar to Fourier basis. So, understanding Fourier basis will also help in DCT understanding.

	- ### FOURIER BASIS:
	- 
		
- ### My Understanding And Observations
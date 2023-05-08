Download Link: https://assignmentchef.com/product/solved-scicomp-project2
<br>
Among the great pioneers of computational physics was Walther Ritz, who (half a century before the digital computer) invented a computational method for solving tough differential equations that is among the most used today: the <em>Ritz-Galerkin</em>-method. Whether solving quantum systems in Hilbert space or simulating whether a bridge will crash in a storm, his method usually lies underneath.

We will not look at that until later in the course. Instead, we will study the problem he invented it for: The mysterious harmonics of Chladni plates, one of the first and most visually striking experiments that let us <em>see </em>sound.

Ernst Chladni, a musician and physicist from 18<sup>th </sup>century Wittenberg, discovered that driving a metal plate at different frequencies with his violin bow sometimes caused dust to gather

<table width="564">

 <tbody>

  <tr>

   <td width="375">into beautiful patterns. At most frequencies, the dust was just shaken about, but through a systematic approach with sand sprinkled over the plate, he found that the magic happened at certain frequencies, which he carefully drew and collected.</td>

   <td width="189">Chladni’s drawing of resonnance modes he discovered with iron plate, violin bow, and sand.</td>

  </tr>

 </tbody>

</table>

Already at Chladni’s time, it was well-understood why the figures appeared: The special frequencies were <em>resonnances</em>, harmonics inherent to the plate geometry that lead to standing waves. In the <em>nodes </em>(the regions where the wave is zero) the sand settles; everywhere else it is pushed around until finding a nodal region to rest. <a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> But it took over a hundred years before anyone could solve the equations and predict the patterns.

The thin plates are ruled by <a href="https://en.wikipedia.org/wiki/Kirchhoff-Love_plate_theory#Isotropic_plates">Kirchhoff’s dynamics (1850),</a> time-evolved by the <em>biharmonic operator</em>

(1)

similar, but not the same as the wave equation. The resonnance modes are the eigenfunctions of the biharmonic operator, and the resonnance frequencies correspond to the eigenvalues:

<table width="564">

 <tbody>

  <tr>

   <td width="547">∆<sup>2</sup><em>u</em>(<em>x,y</em>) = <em>λu</em>(<em>x,y</em>)under free boundary conditions, subject only to the plate being a solid, elastic object:</td>

   <td width="17">(2)</td>

  </tr>

 </tbody>

</table>

<em>x</em>-boundary:                                                             ) = 0     and

(3)

<em>y</em>-boundary:                                                             ) = 0     and

where <em>µ </em>is an elasticity constant, a material property of the plate.

<h2>2      Data</h2>

The full calculation is beyond the scope of this week:<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a> <strong>You will only need to calculate the resonnance eigenvectors and eigenvalues </strong>from a matrix representation <strong>K </strong>of the biharmonic operator, which you may download here: <a href="http://www.nbi.dk/~avery/teaching/scicomp/2020/Chladni-Kmat.npy">Chladni-Kmat.npy</a> (Python) or <a href="http://www.nbi.dk/~avery/teaching/scicomp/2020/Chladni-Kmat.mat">Chladni-Kmat.mat</a> (Matlab). That is, you will simply be working with the eigenproblem:

<strong>Kx </strong>= <em>λ</em><strong>x                                                                                 </strong>(4)

The matrix representation <strong>K </strong>incorporates also the boundary conditions, so that eigenvectors will be solutions to the full problem.

In Python you load the matrix as Kmat = np.load(“Chladni-Kmat.npy”). From Matlab, you write load(“Chladni-Kmat.mat”), after which Kmat will be defined.

For testing your implementation, you can use the matrices given in <a href="http://www.nbi.dk/~avery/teaching/scicomp/2020/examplematrices.py">examplematrices.py</a> / <a href="http://www.nbi.dk/~avery/teaching/scicomp/2020/examplematrices.m">examplematrices.m.</a> Simply report the results for the highest-numbered matrix that works.

<h3>Visualization</h3>

To show your solutions, download <a href="http://www.nbi.dk/~avery/teaching/scicomp/2020/chladni_show.py">chladni</a> <a href="http://www.nbi.dk/~avery/teaching/scicomp/2020/chladni_show.py">show.py</a> and the data file <a href="http://www.nbi.dk/~avery/teaching/scicomp/2020/chladni_basis.npy">chladni</a> <a href="http://www.nbi.dk/~avery/teaching/scicomp/2020/chladni_basis.npy">basis.npy</a> for Python, and for Matlab: <a href="http://www.nbi.dk/~avery/teaching/scicomp/2020/chladni_show.m">chladni</a> <a href="http://www.nbi.dk/~avery/teaching/scicomp/2020/chladni_show.m">show.m</a> and <a href="http://www.nbi.dk/~avery/teaching/scicomp/2020/chladni_basis.mat">chladni</a> <a href="http://www.nbi.dk/~avery/teaching/scicomp/2020/chladni_basis.mat">basis.mat.</a>

Running chladni show defines the basis set, a 15 × 500 × 500 array of 15 basis functions each defined on a 500 × 500 grid, and the following three functions:

show waves(x,basis set): Shows the actual wavefunction corresponding to coefficient vector x show nodes(x,basis set): Shows the wavefunction zeros, where the sand gathers.

show all wavefunction nodes(T,lambdas,basis set): Shows the zeros of all the eigenfunctions defined by the columns of T.

<h2>3       Questions for Week 3</h2>

<ol>

 <li>(1) Implement a function centers,radii = gershgorin(A) that locates the eigenvalues of a matrix using Gershgorin’s theorem. (2) Localize the eigenvalues of <strong>K</strong>, and report the disk centers and radii.</li>

 <li>(1) Implement a function lambda = rayleigh qt(A,x), which takes a matrix <strong>A </strong>and approximate eigenvector <strong>x</strong>, and returns the approximate eigenvalue <em>λ </em>given by the Rayleigh quotient.

  <ul>

   <li>Implement a function x, k = power iterate(A,x0) for power iteration, which takes a matrix <strong>A </strong>and an initial vector <strong>x</strong><sub>0 </sub>as arguments, and returns an eigenvector <strong>x </strong>together with the number <em>k </em>of iterations used. Don’t forget to choose and implement a suitable convergence criterion.</li>

   <li>Test it by finding the largest eigenvalue of the example matrices. Report the eigenvalue found, the Rayleigh residual, and the number <em>k </em>of iterations used.</li>

   <li>What is the largest eigenvalue of <strong>K</strong>? Visualize your eigenfunction using show waves(x,basis set) to see the wave, and show nodes(x,basis set) to see where the sand will gather. The eigenfunction for the largest eigenvalue should have nodes along an 8 × 8 grid.</li>

  </ul></li>

 <li>(1) Write a Rayleigh quotient iteration function x, k = rayleigh iterate(A,x0, shift0), which takes a matrix <strong>A</strong>, an initial vector <strong>x</strong><sub>0</sub>, and an approximate eigenvalue shift<sub>0 </sub>as arguments and returns an eigenvector <strong>x </strong>together with the number <em>k </em>of iterations used.</li>

</ol>

The multiplication by the inverse matrix should be implemented using either your own LUfactorization from as x = lu solve(A,y) or QR-factorization from as x = qr solve(A,y).

<strong>NB: </strong>If you did not get either to work in previous weeks, you can use an in-built linear solver and make a small note that you do this.

<ul>

 <li>Test it with the example matrices, and report the eigenvalues found, Rayleigh residual, and the number <em>k </em>of iterations used.</li>

</ul>

<ol>

 <li>An important feature of inverse iteration and Rayleigh-iteration is the ability to calculate <em>any </em>eigenvalue and its eigenvectors: given an approximate starting point, we obtain an eigenvector to the nearest eigenvalue.

  <ul>

   <li>Use your Rayleigh quotient iteration function together with the Gershgorin centers to calculate as many eigenvectors and eigenvalues of <strong>K </strong>as you can. Are you able to get all of them? Why? If not, find the remaining one(s) by any means necessary. Check using show nodes(x,basis set) that the eigenfunction with lowest eigenvalue looks like a cross:</li>

   <li>Construct the transformation matrix <strong>T </strong>whose columns are the eigenvectors in order of ascending eigenvalues, and check that <strong>K </strong>= <strong>T</strong>Λ<strong>T</strong><sup>−1 </sup>with diagonal Λ.<a href="#_ftn3" name="_ftnref3"><sup>[3]</sup></a> (3) Visualize your solutions using the provided function show all wavefunction nodes(T,lambdas,basis set).</li>

  </ul></li>

</ol>

<a href="#_ftnref1" name="_ftn1">[1]</a> The same principle is used today with 3-dimensional sound waves in air for <em>acoustic levitation</em>.

<a href="#_ftnref2" name="_ftn2">[2]</a> If you are interested in how it is done, <a href="https://www.unige.ch/~gander/Preprints/Ritz.pdf">Gander and Wanner’s From Euler, Ritz, and Galerkin to Modern </a><a href="https://www.unige.ch/~gander/Preprints/Ritz.pdf">Computing</a> has an excellent treatment of the problem. My matrix-representation of the problem, <strong>K</strong>, is calculated by a similar method, with a slightly different and larger basis to yield more modes.

<a href="#_ftnref3" name="_ftn3">[3]</a> You may use the system library inverse for this.
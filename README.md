# Examen_machine_2022

pour la première partie des mesures du temps, dans chacune des images avec un pourcentage de 10

tiny_lena_gray.png

        ➜ mpirun -np 1 fourier_compression.exe data/tiny_lena_gray.png 10
        Caracteristique de l'image : 64x64 => 4096 pixels.
        Nombre de coefficients de fourier restant : 4096
        Fin du programme...
        Temps calcul pour: 
        Function de Fourier: 0.393724
        Function sparse: 0.000763283
        Function de compressing: 0.491142

 small_lena_grey.png

        ➜ ./fourier_compression.exe data/small_lena_gray.png 10
        Caracteristique de l'image : 256x256 => 65536 pixels.
        Nombre de coefficients de fourier restant : 65536
        Fin du programme...
        Temps calcul pour: 
        Function de Fourier: 101.39
        Function sparse: 0.0161419
        Function de compressing: 128.065

### Nous pouvons clairement voir que la fonction de reconstruction d'image prend plus de temps que les autres, nous travaillons donc avec elle.

Nous trouvons les résultats après avoir appliqué la parallélisation omp sur la fonction "inversePartialDiscretTransformFourier"

    Remarque: J'ai converti deux des cycles for de la fonction en un seul cycle avec un artifice de division et de module, afin de réduire le coût de la parallélisation.

tiny_lena_gray.png
  
        ➜ ./fourier_compression.exe data/tiny_lena_gray.png 10       
        Caracteristique de l'image : 64x64 => 4096 pixels.
        Nombre de coefficients de fourier restant : 4096
        Fin du programme...
        Temps calcul pour: 
        Function de Fourier: 0.391267
        Function sparse: 0.000761735
        Function de compressing: 0.219532
        small_lena_gray.png

small_lena_grey.png

        ➜ ./fourier_compression.exe data/small_lena_gray.png 10
        Caracteristique de l'image : 256x256 => 65536 pixels.
        Nombre de coefficients de fourier restant : 65536
        Fin du programme...
        Temps calcul pour: 
        Function de Fourier: 103.238
        Function sparse: 0.0179802
        Function de compressing: 42.0773        

Elle était en effet possible de paralléliser la fonction avec omp qui, comme nous le savons, est très bien utilisé avec les boucles.
    

## Remarque:
- La version 1 n'est que le calcul du temps en code séquentiel.
- La version 2 est une parallélisation de la fonction avec omp.
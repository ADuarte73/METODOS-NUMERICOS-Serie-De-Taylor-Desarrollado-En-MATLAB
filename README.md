# METODOS-NUMERICOS-Serie-De-Taylor-Desarrollado-En-MATLAB
Codigo Realizado -- Para el Desarrollo de Serie de Taylor


----------Script---------------------

 

%pp=input('ingrese p')

xi=input('ingrese valor de xi: ')                 %valor de xi que da el problema 

ximasuno =input('ingrese valor de xi+1: ')           %valor de xi+1 que da el problema 

syms x

n=input('Numero de Repeticiones: ')    +1           %cantidad de repeticiones 

syms

funcion= [-0.1*x^4,-0.15*x^3,-0.5*x^2,-0.25*x+1.2]    %ingresar la funcion, separando los terminos por ","

valh=ximasuno-xi

derivadas = sym('derivadas',[n length(funcion) ])           %matriz que almacena las derivadas de la funcion

iteraciones = linspace(x,x,n)                                                     %derivadas almacenadas en un solo vector

for i=1:n 

                for j=1:length(funcion)

                               if (i==1)

                                               derivadas(i,j)=diff(funcion(j))

                               else

                                               derivadas(i,j)=diff(derivadas(i-1,j))

                               end 

                j=j+1

                end

                iteraciones(i) = sum(derivadas(i,:))

                i=i+1

end

derivadas

valorVerdadero=sum(subs(funcion,x,ximasuno))

syms h

factorial =linspace(0,0,n)

maclaurin =linspace(h,h,n)

for i=1: n

                temp=1

                for j=1:i

                               temp=temp*j

                               j=j+1

                end

                factorial(i)= temp

                maclaurin(i)=h^i/temp

                i=i+1

end

taylor=(maclaurin  .* iteraciones) 

taylor(n+1)=sum(funcion)

respuestah = sum(subs(taylor,h,valh)) %muestra la respuesta dejando expresado h

respuestaX = sum(subs(taylor,x,xi))      %muestra la respuesta dejando expresado x

respuestaFinal = sum(subs(respuestah , x, xi))

formula(1) = taylor(length(taylor))

tabla(1,1) = subs(formula(1),x,xi)

for i=1:length(taylor)-1

                formula(i+1) = taylor(i)

                tabla(i+1,1) = subs(taylor(i),x,xi)

                tabla=subs(tabla,h,valh)

                tabla(i+1,2) = (respuestaFinal - tabla(i+1,1))/respuestaFinal

                tabla(i+1,3) = (tabla(i+1,1) - tabla(i,1))/tabla(i+1,1) 

end

TablaResultados=double(tabla)

TablaResultados

for i=1: length(TablaResultados)-1

                DATOS(i,1)= TablaResultados(i+1,1)

if i==1

DATOS(1,2)=sum(subs(funcion,x,xi))

DATOS(1,5)=abs(valorVerdadero - DATOS(1,2) )

else

DATOS(i,2) = DATOS(i-1,1)+ DATOS(i-1,2)

DATOS(i,5)=abs(valorVerdadero - DATOS(i,2))

end

DATOS(i,3) = (valorVerdadero - DATOS(i,2)) / valorVerdadero

DATOS(i,4) = DATOS(i,3) *100

end

clc

fprintf('Funcion a evaluar= ')

fprintf('%s ', funcion)

fprintf('\nValor de xi: %f  \nValor de xi+1: %f  \nValor de H (xi+1 - xi): %f \nRepeticiones: %f \n\n',xi,ximasuno,valh, n)

for i=1:n

                fprintf('derivada No %d:  %s \n' ,i , iteraciones(i))

                

end

fprintf('\nSerie de Taylor: ')

fprintf('+  %s  ', formula) 

fprintf('\nEstimacion#%d  n=%f  : %s = %f \n',1,0, sum(funcion) , sum(subs(funcion,x,xi)))

for i=1:length(taylor)-1

                fprintf('Estimacion#%d  n=%f : %s = %f \n',i+1,i , taylor(i), TablaResultados(i+1,1))

end

%fprintf('\nValorAproximado - Et(Porcentaje Error Total) - Ea(Porcentaje Error normalizado) \n')

DATOS

fprintf('   F(xi)   |  F(xi+1)    |  ErRel  | ErRelPor | |ET| | \n \n')

%for i=1 : n

%fprintf(' %f  %f  %f  %f  %f \n',DATOS(i,1) ,DATOS(i,2) ,DATOS(i,3) ,DATOS(i,4) ,DATOS(i,5))

%end

fprintf('NOTA:Descripcion de las columnas en la parte de abajo \nEn el valor absoluto no se considera el signo \n')

------------------------FIN DE SCRIPT-----------------------------------------------------------------------------------------------------------------

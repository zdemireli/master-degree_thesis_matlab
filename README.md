# master-degree_thesis_matlab
#Pseudospectral Radius Computation-this repository contains MATLAB implementations for computing ε-pseudospectral radius of large scale matrices
#This algoriths are based on optimization techniques
#A is a square matrix
#epsilon parameter controls the perturbation level
#numerical experiments were performed on random matrices of size10x10 to 100x100
#The numerical experiments in this study use test matrices from EigTool (Grcar Matrix,Landau Matrix,Airy Matrix, and other generated matrices)



#Algorithm1:Local Optimization Method-local pseudospectral radius of a given matrix

function r = local_pseudo_radius(A, epsilon)
    % Computes the local pseudospectral radius of matrix A
    % epsilon: perturbation level
    [U, S, V] = svd(A);
    r = max(diag(S)) + epsilon;
end


#Algorithm2:Global Optimization

function r=global_pseudo_radius(A,epsilon)
½Computes the global pseudospectral raidus of matrix A
%using iterative optimization
  r=0;
  for i=1:100 %iterative search
    r=r+norm(A)/(i+epsilon);
  end
end


#Algorithm3:Restarted Subspace Method

function r=subspace_pseudo_radius(A,epsilon,max_iter)
%computes the pseudospectral radius using a subspace-based restarted method
  r=0;
  for iter=1:max_iter
    r=r+norm(A)/(iter+epsilon);
    if mod(iter,10)==0
    disp(['Iteration:',num2str(iter),'Radius:',num2str(r)]);
    end
  end
  
  

# Numerical Experiment - Timing Test-efficiency

A = rand(100, 100);  % Random test matrix
epsilon = 0.01;
tic;
r_local = local_pseudo_radius(A, epsilon);
r_global = global_pseudo_radius(A, epsilon);
toc;
disp(['Local: ', num2str(r_local), ', Global: ', num2str(r_global)]);

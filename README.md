# Analysis-of-2D-Truss-System-through-the-Global-Stiffness-Matrix-using-MATLAB
This algorithm provides the Nodal Displacement &amp; Nodal Forces of a truss system in 2D after providing the global stiffness, the fixed nodes, the loaded nodes and the load magnitude using MATLAB.

Please cite as: Metry, P. (2023). Analysis of a Truss System in 2D using Manual, Mathematical & Numerical Methods. Coventry University


% Given truss matrix
truss_matrix = [
%% Place your Stiffness Matrix Here
];

% Truss Setup
fixed_nodes = [X, Y, Z]; %% Place your fixed nodes instead of X, Y and Z
loaded_node = L; %% Place your loaded node instead of L
load_magnitude = 0; %% Place the magnitude of your load instead of 0

% Extracting the number of nodes
num_nodes = size(truss_matrix, 1);

% Formulate the global stiffness matrix K
K = truss_matrix;

% Applying boundary conditions
free_nodes = setdiff(1:num_nodes, fixed_nodes);

% Removing rows and columns corresponding to fixed nodes
K_r = K(free_nodes, free_nodes);

% Applying forces (load at node L)
forces = zeros(num_nodes, 1);
forces(loaded_node) = load_magnitude;

% Removing rows corresponding to fixed nodes
F_r = forces(free_nodes);

% Solve for nodal displacements using K_r * U_r = F_r
U_r = K_r \ F_r;

% Assemble the complete displacement vector U
U = zeros(num_nodes, 1);
U(free_nodes) = U_r;

% Calculate nodal forces F = K * U
F = K * U;

% Display results
disp('Number of Nodes:')
disp(num_nodes)

disp('Global Stiffness Matrix:')
disp(K)

disp('Nodal Displacements:')
disp(U)

disp('Nodal Forces:')
disp(F)

# Automated Trajectory Planning: A Cascaded Deep Reinforcement Learning Approach for Low-Thrust Spacecraft Orbit-Raising
We provide the code repository for our paper This repository includes the necessary code to replicate our experiments and utilize our DRL model for spacecraft trajectory planning. By accessing the repository, researchers and practitioners can benefit from our approach to efficiently transfer spacecraft to GEO using low-thrust propulsion systems.

CDRL based GTO to GEO transfer  
<![CDRL based GTO to GEO transfer](https://github.com/talhazaidi13/Cascaded-Deep-Reinforcement-Learning-Based-Multi-Revolution-Low-Thrust-Spacecraft-Orbit-Transfer/blob/main/paper-outputs/GTO-GEO.gif) 



## Files Description

- `config.py`: Contains the configurations or initial parameters to run the code.

- `Scenarios.py`: Contains the parameters for six transfer cases, which are as follows:
    - GTO-1 to GEO_1st network
    - GTO-1 to GEO_2nd network
    - GTO-2 to GEO_1st network
    - GTO-2 to GEO_2nd network
    - Super-GTO to GEO_1st network
    - Super-GTO to GEO_2nd network

- `Spacecraft_env.py`: Contains the gym structured environment, which includes `env.reset()`, `env.step()`, and `env.render()` functions.

- `environment.py`: Contains custom environment functions. These functions in `environment.py` are called by the gym environment in `Spacecraft_env.py`.

- `spacecraftEnivironment.m`: A MATLAB code used to calculate `env.step()` values.

- `environment.yml`: Contains all the required commands to recreate the Conda environment in any local system. This will recreate the exact same environment in which we trained our algorithms.

- `environment_info.txt`: Contains the versions of all installed packages present in our Conda environment.

- `test.py`: Python file which can be used to run the scenerios from pre trained weights.
- `test.sh`: Shell file that contains the code to run test.py file. You can select the case number and max number of episode and all other parameters which are defined in config file in here. <br>
             e.g If you want to run Case 1 i.e 'GTO-1 to GEO_1st network' then in test.sh file you will write as follow:
  ```python
  python test.py  --case 1  --max_nu_ep 100
  ```

- `train.py`: Python file which can be used to train the scenarios from scratch.
- `train.sh`: Shell file that contains the code to run train.py file. You can select the case number and max number of episode and all other parameters which are defined in config file in here. <br>
             e.g If you want to run Case 1 i.e 'GTO-1 to GEO_1st network' then in train.sh file you will write as follow:
  ```python
  python train.py  --case 1 --sh_flag 0
  ```
   Note:  Make sure that while training --sh_flag 0 
- `Final weights` folder: Contains the final trained weights for all six scenarios.
- `CSV Files` folder:  Contains Csv files which is used to communicate between Matlab and python programs data.
- `Plots` : The resulting plots from training or testing the DRL agents will be saved in plots folder.
- `Model_training_weights`: The resulting weights from training the DRL agent will be saved in Model_training_weights folder.
- `Model_training_logs`:    The resulting logs from training the DRL agent will be saved in Model_training_logs folder.

## Setting up Enviornment:


1. Install Conda:        If conda is not installed in your system then install conda. (I used 4.10.1) <br>
2. Install CUDA & CUDNN:  We installed Cuda 11.7.  Follow the instructions in  https://medium.com/geekculture/install-cuda-and-cudnn-on-windows-linux-52d1501a8805#3e72
3. create conda environment named as mat_py3.7 and install python 3.7 in it. 
   ```shell
       conda create --name mat_py3.7 python=3.7
   ```
4. Activate the environment: Use the following command to activate the environment: 
   ```shell                                        
       conda activate mat_py3.7  
   ```
   
5. Install pytorch with gpu: 
    we installed torch 2.0.1+cu117. <br>
    Please follow the instructions as follows to install torch. <br>
        Install PyTorch 2.0.1 with CUDA 11.7:<br>
   ```shell   
   pip install torch==2.0.1+cu117 torchvision==0.15.2+cu117 --extra-index-url https://download.pytorch.org/whl/cu117 
   ```        
   Verify if it installed correctly as follows:<br>
   ```shell   
   python -c "import torch; print(f'Torch Version: {torch.__version__}\nGPU Available: {torch.cuda.is_available()}')"
   ```
   It should show the version as 2.0.1+cu117 and GPU Available: True  (if there is any GPU) <br>

6. Install MATLAB: Install MATLAB on your system. (I am using MATLAB 2021a). If you dont have matlab, you can use the following link to  install MATLAB <br> https://www.mathworks.com/products/new_products/previous_release_overview.html <br>
6a. Navigate to the MATLAB folder: In the activated Conda environment, go to the MATLAB folder by running the following command:
   ```shell   
       cd "<MATLAB_installation_folder>"  
   ```
   Replace <MATLAB_installation_folder> with the path to your MATLAB installation folder. By default, the MATLAB folder is located at "C:/Program Files/MATLAB". Make sure to include the double quotes if the path contains spaces.
6b. Go to the MATLAB Engine Python folder: Change the directory to the MATLAB Engine Python folder by running the following command:
   ```shell
       cd "R2021a\extern\engines\python"  
   ```
   This will navigate you to the relevant folder containing the MATLAB Engine Python setup file.
6c. Install the MATLAB Engine: To install the MATLAB Engine in your Conda environment, execute the setup.py file by running the following command:
   ```shell
       python setup.py install  
   ```
   if this doesnt install directly then open setup.py file and in __main__ replace the version as version="0.1.0" and then save it. 
   after that just run the command in command line "pip install ."
   
   This command will install the MATLAB Engine package in your Conda environment.
6d. Verify the installation: To check if the MATLAB Engine is installed correctly, run the following command:
   ```shell
       python -c "import matlab.engine" 
   ```
   
7. Install git:   - If git is not installed in system then install git ( I used 2.40.0.windows.1)<br>
                    - Download git from  https://git-scm.com/downloads and install it. <br>
                    - While installing: On the "Adjusting your PATH environment" page, select the option "Git from the command line and also from 3rd-party software." This ensures that Git is added to your system's PATH 
                          Environment variable, allowing you to use Git from the command prompt or terminal.<br>
                        - Verify the installation:  After the installation is complete, open a new command prompt or terminal window and run the following command to verify the Git version:
   ```shell
       git --version
   ```
8. Clone the repository: Run the following command in your command prompt or terminal to clone the GitHub repository to your local system:

  ```shell
       git clone https://github.com/talhazaidi13/Cascaded-Deep-Reinforcement-Learning-Based-Multi-Revolution-Low-Thrust-Spacecraft-Orbit-Transfer.git
  ```
   Alternatively, you can just download the code files from the above link. 
            
9. Navigate to the project directory:  Navigate to the project directory on your local system, which contains the cloned repository. In that folder you will find the environment.yml file. you can use the cd command 
                                       to navigate to the folder. e.g if environment.yml is at the location of D:\project then
   ```shell   
       cd "D:\project"
   ```
10. Update conda environment: Update the Conda environment using the environment.yml file. use the following code: <br>
   ```shell
       conda env update -f environment.yml  
   ```
   This command will update the Conda environment based on the specifications in the environment.yml file. <br>
11. Activate the environment: Use the following command to activate the environment: 
   ```shell                                        
       conda activate mat_py3.7  
   ```
   Please note that the name mat_py3.7 is the name of environment specified in the enviornment.yml file. You can rename it according to you.  <br>

## Running the code:
you can run the test.sh or train.sh file  for testing with trained weights and training from the scratch, using the bash command:
```shell
bash test.sh
bash train.sh
```

## Results
CDRL based GTO to GEO transfer  | CDRL based Super-GTO to GEO transfer
:-: | :-:
<image src='/paper-outputs/fig7.PNG' width=500/> | <image src='/paper-outputs/fig13.PNG' width=500/>
<image src='/paper-outputs/tab3.PNG' width=500/> | <image src='/paper-outputs/tab6.PNG' width=500/>
<image src='/paper-outputs/fig5.PNG' width=500/> | <image src='/paper-outputs/fig10.PNG' width=500/>
<image src='/paper-outputs/fig8.PNG' width=500/> | <image src='/paper-outputs/fig11.PNG' width=500/>
<image src='/paper-outputs/fig6.PNG' width=500/> | <image src='/paper-outputs/fig12.PNG' width=500/>

## Citation
If you find this work beneficial to your research or project, I kindly request that you cite it:



## Apendix

%%%% ijcai24.tex
%\documentclass{article}
%pdfpagewidth=8.5in
%\pdfpageheight=11in

% The file ijcai24.sty is a copy from ijcai22.sty
% The file ijcai22.sty is NOT the same as previous years'
%\usepackage{ijcai24}

\documentclass{article}  % Set the font size and document class
\pdfpagewidth=8.5in
\pdfpageheight=11in
% Set standard margins
\usepackage[margin=1in]{geometry}

% Use the postscript times font!
\usepackage{times}
\usepackage{soul}
\usepackage{url}
\usepackage[hidelinks]{hyperref}
\usepackage[utf8]{inputenc}
\usepackage[small]{caption}
\usepackage{graphicx}
\usepackage{amsmath}
\usepackage{amsthm}
\usepackage{booktabs}
\usepackage{algorithm}
\usepackage{algorithmic}
\usepackage[switch]{lineno}

% Adrian's packages
\usepackage{mathtools} % http://ctan.org/pkg/mathtools
\usepackage{array}
\setcounter{MaxMatrixCols}{20} % Increases the number of possible columns in bmatrix
\usepackage{bm,ulem} % For bolded vectors
\usepackage{wasysym} % For moon symbol
\newcommand{\us}{$\mskip3mu$} % For units of measurement skip
\usepackage{adjustbox} % LaTeX, How to fit a large table in a page
\usepackage{xcolor} % For colors
\usepackage{comment} % for \begin{comment} environment

% Talha's packages
\usepackage{multirow}
\usepackage{subfigure}
\bibliographystyle{plain}   % to make references as numbers instead of names
%\bibliographystyle{apalike}
%\usepackage{natbib}

% Comment out this line in the camera-ready submission
\linenumbers

\urlstyle{same}

% the following package is optional:
\usepackage{latexsym}

% Add these lines to force single-column format
\makeatletter
\def\@twocolumnfalse{}
\makeatother



% See https://www.overleaf.com/learn/latex/theorems_and_proofs
% for a nice explanation of how to define new theorems, but keep
% in mind that the amsthm package is already included in this
% template and that you must *not* alter the styling.
\newtheorem{example}{Example}
\newtheorem{theorem}{Theorem}

% Following comment is from ijcai97-submit.tex:
% The preparation of these files was supported by Schlumberger Palo Alto
% Research, AT\&T Bell Laboratories, and Morgan Kaufmann Publishers.
% Shirley Jowell, of Morgan Kaufmann Publishers, and Peter F.
% Patel-Schneider, of AT\&T Bell Laboratories collaborated on their
% preparation.

% These instructions can be modified and used in other conferences as long
% as credit to the authors and supporting agencies is retained, this notice
% is not changed, and further modification or reuse is not restricted.
% Neither Shirley Jowell nor Peter F. Patel-Schneider can be listed as
% contacts for providing assistance without their prior permission.

% To use for other conferences, change references to files and the
% conference appropriate and use other authors, contacts, publishers, and
% organizations.
% Also change the deadline and address for returning papers and the length and
% page charge instructions.
% Put where the files are available in the appropriate places.


% PDF Info Is REQUIRED.

% Please leave this \pdfinfo block untouched both for the submission and
% Camera Ready Copy. Do not include Title and Author information in the pdfinfo section


\title{Automated Trajectory Planning: A Cascaded Deep Reinforcement Learning Approach for Low-Thrust Spacecraft Orbit-Raising}

\iffalse
% Single author syntax
\author{
    First Author
    \affiliations
    Affiliation
    \emails
    email@example.com
}
\fi
% Multiple author syntax (remove the single-author syntax above and the \iffalse ... \fi here)
\iffalse
\author{
First Author$^1$\and
Second Author$^2$\and
Third Author$^{2,3}$\And
Fourth Author$^4$\\
\affiliations
$^1$First Affiliation\\
$^2$Second Affiliation\\
$^3$Third Affiliation\\
$^4$Fourth Affiliation\\
\emails
\{first, second\}@example.com,
third@other.example.com,
fourth@example.com
}
\fi


\makeatletter
\def\@maketitle{
  \begin{center}
    {\LARGE\bf \@title \par}
    \vspace{1.5em}
    {\LARGE\bf Supplementary Material \par} % Add your subtitle here
    \vspace{1em}
    {\large \@author \par}
  \end{center}
  \par
}
\makeatother






\begin{document}
%\begin{multicols}{2} % Specify the number of columns (1 for single-column)

\maketitle


\section{Transfer Scenarios}
The transfer scenarios presented in the paper not only differ in terms of the initial and final orbit but also vary due to the initial spacecraft parameters. These spacecraft parameters play a significant role in trajectory optimization problems. To ensure fair comparisons with other results in the literature, we standardized these parameters based on their values. As a result, we considered three Geostationary Transfer Orbit (GTO) initial orbit scenarios (GTO-1, GTO-2, GTO-3) and two Super-Geostationary Transfer Orbit (Super-GTO and Super-GTO-2) scenarios, as outlined in Table 1 in the main text. The details of these spacecraft parameters are presented in Table~\ref{tab:spac_para}.

\begin{table*}[h]

\centering
% \def\arraystretch{1.4}
% \setlength\tabcolsep{2mm}
% \normalsize
{
  \begin{center}
    \begin{tabular}{|c|c|c| c| c| c |c|}


      \hline  


      \textbf{Scenarios} & 
      \textbf{Impulse I$_{sp}$} &  \textbf{Efficiency $\lambda$} & \textbf{Power P} & 
      \textbf{ Mass m} & \textbf{Thrust F} & \textbf{Thrust during shadows} \\
      \hline

      GTO-1 to GEO &  1800s & 55\% &  5kW & 1200kg & 0.31N & No \\ \hline
      GTO-2 to GEO &  3300s & 65\% &  5kW & 450kg & 0.20N & No \\ \hline
      GTO-3 to GEO &  3000s & - &  - & 2000kg & 0.35N & Yes \\ \hline
      Super-GTO to GEO &  3300s & 65\% &  10kW & 1200kg & 0.40N & No \\ \hline
      Super-GTO-2 to NRHO &  1500s & - &  - & 1000kg & 1N & Yes \\ \hline
     
    \end{tabular}
  

  \end{center}
}
\caption{Spacecraft initial parameters across all transfer scenarios}
  %\vspace{-2.5 mm}
  \label{tab:spac_para}
  %\vspace{-2 mm}
  \vspace{1 mm}
\end{table*}
















\section{CDRL Framework}
In this section we will provide the additional details and calculations for our cascaded deep reinforcement learning framework. 


\subsection{State Elements}
As introduced in the main paper in Section 4.3, our Cascaded Deep Reinforcement Lerning (CDRL) aprroach utilized the five 'he' elements as a state vector which are shown as follows:

\begin{equation}\label{orbital_element_2_2}
\mathbf{s} = \begin{bmatrix} h & h_X & h_Y & e_X & e_Y  \end{bmatrix} ^{T}
\end{equation}

where $h$ denotes the magnitude of angular momentum, while $h_X$ and $h_Y$ denote the component of specific angular momentum along the Earth-centered inertial reference frame and the components of the eccentricity vector $e_x$ and $e_y$ in a non-inertial reference frame obtained after a 2-1 Euler rotation sequence. The initial values of these elements for all scenarios are stated in Tab \ref{tab:he_element}.

\begin{table*}[h]

\centering
% \def\arraystretch{1.4}
% \setlength\tabcolsep{2mm}
% \normalsize
{
  \begin{center}
    \begin{tabular}{|c|c|c c c c c|}
       \hline 
      \multirow{2}{*}{\textbf{Scenarios}} & 
      \multirow{2}{*}{\textbf{Position}}  &
      \multicolumn{5}{c|}{\textbf{State Parameters}} \\  
       &  & \textbf{h (km\textsuperscript{2}/s)} & \textbf{ h\textsubscript{x} (km\textsuperscript{2}/s)} & \textbf{ h\textsubscript{y} (km\textsuperscript{2}/s)} & \textbf{ e\textsubscript{x}} & \textbf{ e\textsubscript{y}} \\ 
      \hline
      
      \multirow{2}{*}{\begin{tabular}[c]{@{}c@{}} GTO-1 - GEO \end{tabular}} & \begin{tabular}[c]{@{}c@{}} Initial  \end{tabular} 
          & 67288.41965 & 0 &-32107.258 &0.7306 &0\\
          & \begin{tabular}[c]{@{}c@{}} Target   \end{tabular} & 29640.2292 & 0 & 0 &0 &0  \\ 
      \hline
 
     
      \multirow{2}{*}{\begin{tabular}[c]{@{}c@{}} GTO-2 - GEO \end{tabular}} & \begin{tabular}[c]{@{}c@{}} Initial  \end{tabular} 
          & 67246.21689 & 0 & -30529.143 &0.7310 &0\\
          & \begin{tabular}[c]{@{}c@{}} Target   \end{tabular} & 29640.2292 & 0 & 0 &0 &0  \\ 
      \hline

      
      \multirow{2}{*}{\begin{tabular}[c]{@{}c@{}} GTO-3 - GEO \end{tabular}} & \begin{tabular}[c]{@{}c@{}} Initial  \end{tabular} 
          & 68196.3519 & 0 &-8311.044 &0.725 &0\\
          & \begin{tabular}[c]{@{}c@{}} Target   \end{tabular} & 29640.2292 & 0 & 0 &0 &0  \\ 
      \hline
      
      \multirow{2}{*}{\begin{tabular}[c]{@{}c@{}} Super-GTO - GEO \end{tabular}} & \begin{tabular}[c]{@{}c@{}} Initial  \end{tabular} 
          & 70532.88179 & 0 &-26991.765 &0.8705 &0\\
          & \begin{tabular}[c]{@{}c@{}} Target   \end{tabular} & 29640.2292 & 0 & 0 &0 &0  \\ 
      \hline

      \multirow{2}{*}{\begin{tabular}[c]{@{}c@{}} Super-GTO-2 - NRHO \end{tabular}} & \begin{tabular}[c]{@{}c@{}} Initial  \end{tabular} 
          & 101055.564 & 8993.124 & -44988.209 &0.6342 & 0.1422  \\ 
          & \begin{tabular}[c]{@{}c@{}} Target   \end{tabular} 
          & 384073.943 & 43240.356 & -111563.294 &-0.0209 &-0.1249\\
      \hline


    \end{tabular}
  \end{center}
}
\caption{State parameters (he) defined for all transfer scenarios}
  %\vspace{-2.5 mm}
  \label{tab:he_element}
  %\vspace{-2 mm}
  \vspace{1 mm}
\end{table*}


\subsection{Convergence Parameters}
In Section 4.3, we examine five pivotal terminal conditions at each time step, which are integral spacecraft orbital elements: eccentricity ($e$), semi-major axis ($a_\text{sm}$), inclination ($i$), right ascension of the ascending node ($\Omega$), and argument of periapsis ($\omega$). These orbital elements are derived from the state ($he$) elements, as defined in Eq. \ref{orbital_element_2_2}. The conversion of these state elements to orbital elements for convergence assessment proves advantageous, particularly in GEO transfer scenarios where only three orbital elements (eccentricity ($e$), $a_\text{sm}$, and inclination ($i$), as detailed in Table 2 of the main text) are required for convergence. This transformation from five to three state elements significantly mitigates the non-linearity of the problem, enhancing convergence and optimizing results. This transformation is also noteworthy in NRHO transfer scenarios, where the convergence of these three orbital parameters substantially influences the remaining two orbital parameters (RAAN, argp) as well.

The computation for converting $he$ elements to orbital state elements is delineated as follows:



The first condition checks the eccentricity of the spacecraft's orbit. The magnitude of eccentricity is calculated from the $e_x$ and $e_y$ parameters, which are part of the state vector. Here $e_{tol}$ denotes the tolerance value for eccentricity.
\begin{eqnarray}\label{e}
e_{tar} \leq \left[\textbf{e}= \sqrt{e_{x}^2 + e_{y}^2} \, \right] \leq e_{tar} + e_{tol}
\end{eqnarray}

The second condition checks the semi-major axis of the spacecraft's orbit, as shown in Eq.~(\ref{action_eq_2}). The semi-major axis ($a_\text{sm}$) is calculated using the $h$, $e_x$, and $e_y$ parameters from the state vector, as well as the gravitational parameter $\mu$. The value of a$_\text{sm}^{\text{tar}}$ is the desired target value for the semi-major axis, and a$_\text{sm}^{\text{tol}}$  is the tolerance value for the semi-major axis.
\begin{eqnarray}\label{a}
\text{a}_\text{sm}^\text{tar} - \text{a}_\text{sm}^\text{tol}  \leq \left[ \text{a}_\text{sm} =  \frac{h^2 }{\mu (1 - \sqrt{(e_{x}^2 - e_{y}^2))}} \right] \leq \text{a}_\text{sm}^\text{tar} +\text{a}_\text{sm}^\text{tol} 
\end{eqnarray}



The third condition checks the inclination angle of the spacecraft's orbit, as shown in Eq.~(\ref{action_eq_3}), where \textit{$i_{tol}$} denotes the tolerance value for the inclination angle.

\begin{eqnarray}\label{i}
i_{tar} \leq \left[i= \sqrt{\frac{h_{x}^2 + h_{y}^2 }{h}}\,\right] \leq i_{tar} + i_{tol}
\end{eqnarray}

 
The fourth condition assesses the right ascension of the ascending node (RAAN), denoted as ($\Omega$). The calculation involves first determining the vertical component $h_{z}$, which is then utilized to find the value of $\Omega$. The computation steps for finding $\Omega$ and establishing the tolerance ranges, $\Omega_{tol}$, are detailed as follows:


\begin{eqnarray}\label{RAAN_main}
%0 \leq \left[\textbf{e}= \sqrt{e_{x}^2 + e_{y}^2} \, \right] \leq e_{tol}
%A = e_{x} \sin{\phi} - e_{y} \cos{\phi} \\
%B =1 + e_{x} \cos{\phi} + e_{y} \sin{\phi} \\
hz = \sqrt{h^2 - h_{x}^2 - h_{y}^2} \quad
% N = \left[h_{x}, h_{y}, h_{z}\right] \\
n= cross\left(\begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}, \begin{bmatrix} h_x \\ h_y \\ h_z \end{bmatrix}\right)  \\ 
\Omega =\begin{cases}
\arccos\left(\frac{n(1)}{\|\mathbf{n}\|}\right), & \text{if } n(2) \geq 0 \\
360 - \arccos\left(\frac{n(1)}{\|\mathbf{n}\|}\right), & \text{otherwise}
\end{cases} \\
\Omega_{tar}-\Omega_{tol} \leq \Omega  \leq \Omega_{tar}   \label{RAAN}
\end{eqnarray}


The fifth condition evaluates the argument of periapsis ($\omega$). Unlike other parameters, this parameter cannot be directly computed from the $he$ elements. Instead, additional calculations are required to first calculate the rotation matrix and then it determine the value of ($\omega$). The subsequent calculations, along with the corresponding tolerance settings, are outlined as follows:

\begin{eqnarray}\label{argpmain}
% Rotations from I (ECI) to I' to O
\zeta = \arctan\left(\frac{h_x}{h_z}\right);  \quad
\eta = -\frac{h_y}{h}; \quad
\eta_{\text{cos}} = \sqrt{\frac{h^2 - h_y^2}{h^2}};\\
R_{\zeta} = \begin{bmatrix}
  \cos(\zeta) & 0 & -\sin(\zeta) \\
  0 & 1 & 0 \\
  \sin(\zeta) & 0 & \cos(\zeta)
\end{bmatrix};\quad  % Rotation matrix for angle zeta\\
R_{\eta} = \begin{bmatrix}
  1 & 0 & 0 \\
  0 & \eta_{\text{cos}} & \eta \\
  0 & -\eta & \eta_{\text{cos}}
\end{bmatrix}; \\% Rotation matrix for angle eta\\
R_{\text{ECI to R}} = R_{\eta} \cdot R_{\zeta};\quad
\mathbf{e}_{ECI} = \mathbf{R}_{ECI to R}^T \begin{bmatrix} e_x \\ e_y \\ 0 \end{bmatrix}; \\
\omega =\begin{cases} \arccos\left(\frac{\mathbf{n} \cdot \mathbf{e}_{ECI}}{\|\mathbf{n}\| \cdot \|\mathbf{e}_{ECI}\|}\right), & \text{if } e_{ECI}(3) \geq 0 \\
360 - \arccos\left(\frac{\mathbf{n} \cdot \mathbf{e}_{ECI}}{\|\mathbf{n}\| \cdot \|\mathbf{e}_{ECI}\|}\right), & \text{otherwise} 
\end{cases} \\
\omega_{tar} \leq \omega  \leq \omega_{tar} + \omega_{tol} \label{argp}
\end{eqnarray}

The tolerance ranges and target values for all of these parameters in Eq.(\ref{e},\ref{a},\ref{i},\ref{RAAN},\ref{argp}) are presented in Table 2 in the main text.


\subsection{Reward Weights} \label{sub:RW}    

We introduced the gradient-aided reward function in our approach, elaborated in Section 4.3 of the main text. The reward function incorporates user-defined weights, which are presented in Table \ref{tab:weights}. These weights are represented by $W=[w_{1}; w_{2}; w_{3}]$, where $W[:,1]$ corresponds to the weightage of $a_\text{sm}$, $W[:,2]$ pertains to the weightage of $e$, and $W[:,3]$ reflects the weightage of $i$ in Eq.~16 (main text). These weight assignments are aligned with the first, second, and third columns of Table \ref{tab:weights}, respectively. We also fixed the value of $\tau$ in Eq.~16 (main text) as 0.5. The rewards weights are shown as follows:


\begin{table}[h]
% \def\arraystretch{1.7}
% \setlength\tabcolsep{2mm}
% \normalsize

\centering
{
    \begin{tabular}{|c|c c c |c c c | c c c |}
      \hline  
      \textbf{}  & 
      \multicolumn{3}{c|}{\textbf{GTO to GEO}} & 
      \multicolumn{3}{c|}{\textbf{Super-GTO to GEO }} & 
      \multicolumn{3}{c|}{\textbf{Super-GTO-2 to NRHO }} \\ 
      
      \textbf{} & 
      \textbf{$W[:,1]$} &  \textbf{W$[:,2]$} & \textbf{W$[:,3]$} & 
      \textbf{ $W[:,1]$} & \textbf{$W[:,2]$} & \textbf{W$[:,3]$} & 
      \textbf{ $W[:,1]$} & \textbf{$W[:,2]$} & \textbf{W$[:,3]$}   \\
      \hline
      
       \textbf{w$_{1}$}   & 1e$^{3}$  & 2e$^{3}$ & 3e$^{2}$ & 
                          1e$^{3}$  & 4e$^{3}$ & 3e$^{2}$  &  
                          8e$^{5}$  & 8e$^{5}$ & 8e$^{5}$      \\ \hline
                          
       \textbf{w$_{2}$}   & 1e$^{-2}$  & 1.9e$^{-7}$  & 3e$^{-5}$ &
                            1e$^{-2}$  & 1.9e$^{-9}$  & 3e$^{-5}$ &
                            3e$^{1}$  & 3e$^{1}$  & 3e$^{1}$ \\ \hline 
                            
       \textbf{w$_{3}$}   & 5e$^{2}$  & 7e$^{2}$  & 3e$^{2}$ &
                            5e$^{2}$  & 2e$^{3}$  & 3e$^{2}$ &
                            1e$^{2}$  & 1e$^{2}$  & 1e$^{2}$  \\ \hline 
    \end{tabular}
}
  % \vspace{1 mm}
\caption{ Weights (W$=[w_{1};w_{2};w_{3}]$) used in calculating the reward function.}
  %\vspace{-2.5 mm}
  \label{tab:weights}
\end{table}






\section{Implementation Details}

In this section, we present the dynamic model assumptions in Section~\ref{modass}, eclipse model assumptions in Section~\ref{eclipse}, and hyperparameter settings in Section 3.3. The information is intended to offer comprehensive details to facilitate result replication by any interested party. The complete implementation code is also accessible at the following link: \underline{\url{https://github.com/talhazaidi13/Automated-Trajectory-Planning--CDRL-based.git}}.



\subsection{Modeling Assumptions} \label{modass}
We assume constant spacecraft thrust, excluding periods in Earth's shadow. Modeling assumptions for the spacecraft's dynamic model include neglecting orbital perturbations and radiation damage. Specifically, we focus on onboard thrust as the sole force, ignoring additional perturbations and assuming constant thrust during the Sun-lit trajectory. These simplifications enable a fair comparison with existing sequential and DRL approaches in the literature. Incorporating orbital perturbations or radiation damage can be done by adding corresponding terms to the model.

In our modeling approach, we maintain the assumption of constant spacecraft thrust, with exceptions only during the spacecraft's passage through the Earth's shadow. Our dynamic model incorporates certain assumptions to streamline the analysis. Firstly, we neglect the influence of orbital perturbations in this paper. While the force terms in Eq 8 (main text) can encompass various forces acting on the spacecraft (thrust, J2 perturbation, gravitational forces) we specifically consider the force to be solely due to onboard thrust.
Secondly, we disregard the impact of radiation damage in this paper. In actuality, the spacecraft's solar arrays may experience degradation when traversing the Van Allen belts, leading to a reduction in available thrust. However, we simplify our model by assuming constant thrust during the Sun-lit portion of the trajectory, overlooking the radiation damage effects.
These modeling assumptions are made for the purpose of facilitating a fair comparison with the sequential approach \cite{sreesawet2018fast} and a previously studied Deep Reinforcement Learning (DRL) approach \cite{kwon2021autonomous} found in the literature. It is important to note that if one wishes to incorporate orbital perturbations into the problem, additive terms representing those perturbations need to be included in Eq 8 (main text). Similarly, for those interested in considering the effect of radiation damage, an artificial neural network-based radiation damage prediction can be integrated into the framework.






\subsection{Eclipse Model Assumptions} \label{eclipse}

As the spacecraft undergoes multiple revolutions around the Earth to reach its final orbit employing all-electric propulsion, it is highly likely to traverse the Earth's shadow. During these shadow passages, the spacecraft has the option to utilize onboard batteries to power the thrusters or switch them off and coast. This study assumes coasting during the spacecraft's passage through the Earth's shadow in GEO transfer scenarios.

To identify the regions where the spacecraft enters the Earth's shadow, a shadow model is required. In this work, we employ the cylindrical eclipse model. The cylindrical Earth shadow model assumes that the shadow cast by Earth is cylindrical in shape and remains fixed in space without movement. The conditions to determine whether the spacecraft is in eclipse are defined as follows:

\begin{align}
    X_{I} &< 0, \\
    \sqrt{Y^2_{I} + Z^2_{I}} &< R_{E}  
\end{align}

where $X_I$, $Y_I$, and $Z_I$ represent the components of the Cartesian position vector of the spacecraft in the Inertial frame, and $R_E$ is the radius of the Earth. The equations to convert the spacecraft's state vector, as utilized in this work, to Cartesian coordinates are discussed in~\cite{sreesawet2018fast}.



\begin{table*}[h]

\centering
% \def\arraystretch{1.4}
% \setlength\tabcolsep{2mm}
% \normalsize
{
  \begin{center}
    \begin{tabular}{|c|c|}
       \hline 

             \textbf{Learning rate}   & $3\exp{-4}$ \\ \hline
            \textbf{Discount factor}   & $0.99$   \\ \hline                     
            \textbf{Buffer size}   & $1\exp{6}$  \\ \hline
            \textbf{Time Penalty } $\tau$   & $0.5$  \\ \hline
    \end{tabular}
  \end{center}
}

\caption{Hyper-parameters settings used in CDRL Training.}
  %\vspace{-2.5 mm}
  \label{tab:param2}
  %\vspace{-2 mm}
  \vspace{1 mm}
\end{table*}







\subsection{CDRL Parameters settings} \label{hyper1}

We conducted experiments on an Intel(R) Xeon(R) CPU E5-1620 v4 operating at a frequency of 3.5GHz with 8 cores, coupled with the NVIDIA GeForce GTX 1080 graphics processing unit (GPU), and 32GB of random access memory (RAM) to meet the computational requirements. The implementation of our Cascaded Deep Reinforcement Learning (DRL) algorithms was carried out in Python 3.7 using the PyTorch framework, and built up over the Soft Actor-Critic implementation by stable-baselines. This hardware/software configuration significantly contributed to the efficient and effective development and training of our models. The hyperparameters for our actor, critic, and target critic models are presented in Table \ref{tab:param}

\begin{table*}[h]

\centering
% \def\arraystretch{1.4}
% \setlength\tabcolsep{2mm}
% \normalsize
{
  \begin{center}
    \begin{tabular}{|c|c c |c c| c c|}
       \hline 
      \multirow{2}{*}{\textbf{Layers}} & 
      \multicolumn{2}{c|}{\textbf{Actor}} & 
      \multicolumn{2}{c|}{\textbf{Critic}} & 
      \multicolumn{2}{c|}{\textbf{Target Critic}}\\  

      
                                                & 
       \textbf{Size} & \textbf{Activation Fun.} &
       \textbf{Size} & \textbf{Activation Fun.}&
       \textbf{Size} & \textbf{Activation Fun.}
       \\  \hline

      \textbf{Input layer}   & $6$  & ReLU &
                            $8$  & ReLU & 
                            $8$  & ReLU     \\ \hline

    \textbf{Hidden 1}   & $256$  & ReLU &
                            $256$  & ReLU & 
                            $256$  & ReLU    \\ \hline
                            
    \textbf{Hidden 2}   & $256$  & ReLU &
                            $256$  & ReLU & 
                            $256$  & ReLU    \\ \hline

           \textbf{output}   & $2$  & ReLU &
                            $1$  & Linear & 
                            $1$  & Linear     \\ \hline
      

    \end{tabular}
  \end{center}
}

\caption{Network parameters used in CDRL.}
  %\vspace{-2.5 mm}
  \label{tab:param}
  %\vspace{-2 mm}
  \vspace{1 mm}
\end{table*}




The actor network outputs the mean ($\mu$) and variance ($\sigma$) for each action, with the state values as input. Utilizing these mean and variance values, the actor network generates a Gaussian distribution and samples actions from it. Additionally, it produces the log probabilities of the sample distribution to calculate the entropy. The other hyper-parameters utilized in the CDRL training are presented in table \ref{tab:param2}







\section{Additional Training Results}
In this section, we present the convergence scores and converging time plots during the training of CDRL networks for two-body scenarios. It's important to note that in the main text, we exclusively showcased these convergence plots for three-body scenarios due to space limitations. As illustrated in Fig.~\ref{fig:GTOReturn} and Fig.~\ref{fig:SGTOReturn}, it is evident that as the training score increases, the episodic time for the converged episodes decreases. We continued the training of DRL networks until we achieved convergence in episodes along with stable high scores.




\begin{figure}[H]
    \centering
    \newcommand{\ww}{0.35}
    \subfigure[DRL-1 Episodic Return]{\includegraphics[width=\ww\textwidth]{Figures/GTO_Scores_drl1.jpg}} 
    \subfigure[DRL-2 Episodic Return]{\includegraphics[width=\ww\textwidth]{Figures/GTO_Scores_drl2.jpg}} 
    \subfigure[DRL-1 Flight Time]{\includegraphics[width=\ww\textwidth]{Figures/GTO_time_drl1.jpg}} 
    \subfigure[DRL-2 Flight Time]{\includegraphics[width=\ww\textwidth]{Figures/GTO_time_drl2.jpg}} 
    \vspace{-1.5 mm}
    \caption{Episodic return and convergence times over training steps for GTO to GEO transfer scenario. DRL-1 and DRL-2 represent the two cascaded DRL agents. Episodic return is for all training episodes, whereas the flight time is for converged episodes during the training.}
    \label{fig:GTOReturn}
    \vspace{-2 mm}
\end{figure}


\begin{figure}[H]
    \centering
    \newcommand{\ww}{0.35}
    \subfigure[DRL-1 Episodic Return]{\includegraphics[width=\ww\textwidth]{Figures/SGTO_Scores_drl1.jpg}} 
    \subfigure[DRL-2 Episodic Return]{\includegraphics[width=\ww\textwidth]{Figures/SGTO_Scores_drl2.jpg}} 
    \subfigure[DRL-1 Flight Time]{\includegraphics[width=\ww\textwidth]{Figures/SGTO_time_drl1.jpg}} 
    \subfigure[DRL-2 Flight Time]{\includegraphics[width=\ww\textwidth]{Figures/SGTO_time_drl2.jpg}} 
    \vspace{-1.5 mm}
    \caption{Episodic return and convergence times over training steps for Super-GTO to GEO transfer scenario. DRL-1 and DRL-2 represent the two cascaded DRL agents. Episodic return is for all training episodes, whereas the flight time is for converged episodes during the training.}
    \label{fig:SGTOReturn}
    \vspace{-2 mm}
\end{figure}






\iffalse
The actor network, depicted in Figure 1 in the main text, does not explicitly show the mean and variance parts due to space limitations. This is clarified in the accompanying Figure \ref{actor} as follows.


\begin{figure}[h]

  \centering
  \includegraphics[scale =1]{Figures/actor.jpg}
  %  \vspace{-15pt}
  \caption{Actor Network shows the }
  \label{actor}
\end{figure}

\fi




























%% The file named.bst is a bibliography style file for BibTeX 0.99c
\bibliographystyle{named}
\bibliography{ijcai24}

%\end{multicols}
\end{document}






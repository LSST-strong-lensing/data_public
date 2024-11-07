# Line of Sight External Convergence and Shear Distributions Files

## SLSim defaults Contains:
*   `no_nonlinear_distributions.h5  `: 
Contains the joint external convergence and shear distributions for the line of sight, without the non-linear correction*.

* To use the distributions, when using class `LensPop` from `lens_pop.py` or class `Lens` form `lens.py`, it is default set: 
  * `los_bool` parameter to `True` 
  * `nonlinear_los_bool` parameter to `False` 
  
  to use this distribution.

## Additional files Contains:

* You can add the file    `joint_distribution.h5  ` in the same file folder (usually \data\glass), which contains the joint external convergence and shear distributions for the line of sight, with the non-linear correction*.

* To use the distributions, after put the `joint_distribution.h5  ` in the folder, when using class `LensPop` from `lens_pop.py` or class `Lens` form `lens.py`,you can set:
  *  `los_bool` parameter to `True` 
  * `nonlinear_los_bool` parameter to `True`
  
  to use the non-linear corrected distributions.


### Adding other distributions:
You can add other files such as  `joint_distributions_sigma8_0.810.h5` or `no_nonlinear_distributions_sigma8_0.810.h5` ....
  * To using the distributions from this file, when using class `LensPop` from `lens_pop.py` or class `Lens` form `lens.py`: 
    * `los_bool` parameter to `True` 
    * `nonlinear_los_bool` parameter to `True` or `False` based on which kind of file you want to use.
    * `nonlinear_correction_path` or/and `no_correction_path` parameter to the file path of the file you want to use.
    *  For example, if you are trying to use 
    `joint_distributions_sigma8_0.810.h5` and `no_nonlinear_distributions_sigma8_0.810.h5` files in one of the notebook in the `slsim/notebook`, you can set the file path as follows:
    ```
    import os
    from slsim.lens_pop import LensPop

    current_script_path = os.getcwd()
    current_directory = os.path.dirname(current_script_path)
    
    nonlinear_correction_path = os.path.join(
                    current_directory, 
                    "data/glass/joint_distributions_sigma8_0.810.h5"
    )
    no_correction_path = os.path.join(
                    current_directory,
                    "data/glass/no_nonlinear_distributions_sigma8_0.810.h5"
    )
    
    los_config_using_nonlinear_los=LOSConfig(
    los_bool=True, #
    nonlinear_los_bool = True,
    nonlinear_correction_path=nonlinear_correction_path,
    no_correction_path=None,
    )

    # Using the non-linear corrected distributions:
    gg_lens_pop_using_nonlinear_corrected_los = LensPop(
    deflector_population=lens_galaxies,
    source_population=source_galaxies,
    cosmo=cosmo,
    sky_area=sky_area,
    los_config=los_config_using_nonlinear_los_bool,
    )



    ```

***

### *Non-linear correction: 
For external convergence $\kappa_{ext}$ as follows:

$$
1 - \kappa_{ext} = \frac{(1-\kappa_d)(1-\kappa_s)}{1-\kappa_{ds}}
$$

Additionally, computed the external shear $\gamma_{ext}$ :

$$
\gamma_{ext} = \sqrt{(\gamma_{d1}+\gamma_{s1}-\gamma_{ds1})^2+(\gamma_{d2}+\gamma_{s2}-\gamma_{ds2})^2}
$$

where $\kappa_d$, $\kappa_s$, $\kappa_{ds}$, $\gamma_{d1}$, $\gamma_{d2}$, $\gamma_{s1}$, $\gamma_{s2}$, $\gamma_{ds1}$, and $\gamma_{ds2}$ are the convergence and shear components of the observer-deflector, observer-source, and deflector-source systems, respectively.

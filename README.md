## densityPeak project description


### Installation
    pip install iceDP

### Import
    import iceDP

### Usage
    x=iceDP.main_procedure.bunchDots()
    x.readData('/Users/lhlin/ruhai/proj/density_peak/data/chr4_chr11.txt')
    x.get_rho()
    x.get_delta()
    x.do_chi_square_test()
    x.define_border()
    x.horizontal_and_vertical_fold_change()
    iceDP.main_procedure.save_reult(x, 'chr4_chr11_DPresult')
* plot
    iceDP.plot_spots.plot_one_spot(x.data_filted2.values[1], x)

### version scheme
> * Increment the MAJOR version when you make incompatible API changes.
> * Increment the MINOR version when you add functionality in a backwards-compatible manner.
> * Increment the PATCH version when you make backwards-compatible bug fixes.
>   [(Source)](https://semver.org/)




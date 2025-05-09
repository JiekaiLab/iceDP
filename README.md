
## densityPeak project description


### Installation
way one
copy to ${python_path}/site-packages

way two
    pip install iceDP  # not up load yet

### Import
    import iceDP

### Usage
* data processing

    x=iceDP.main_procedure.bunchDots()
    x.readData('play_data/chr4_chr11_mm10.txt')
    x.get_rho()
    x.get_delta()
    x.do_chi_square_test()
    x.define_border()
    x.horizontal_and_vertical_fold_change()
    iceDP.main_procedure.save_reult(x, 'chr4_chr11_mm10_DPresult')

* plot

    iceDP.plot_spots.plot_one_spot(x.data_filted2.values[1], x)



=======
# iceDP
Identifier of inter-chromatin interaction based on density peak.



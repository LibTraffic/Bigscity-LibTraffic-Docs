# The Implemented Dataset Class

Here we introduce the functions of several dataset classes that have been implemented.

- `AbstractDataset`

  Base class for all dataset classes. **Note that this is an abstract class and can not be used directly.**

- `TrajectoryDataset`

  Base class for all trajectory location prediction tasks.

- `TrafficStateDataset`

  One of base class for all traffic state prediction tasks. **Note that this is an abstract class and cannot be used directly.** By default, the data of `input_window` is used to predict the data corresponding to `output_window`. The [Batch](../data/batch.md) object generated by this class contains two keys, one `X` and one `y`. Here `input_window` and `output_window` are parameters for data, see [here](../data/args_for_data.md) for details. 

- `TrafficStateCPTDataset`

  Another base class for all traffic state prediction tasks. **Note that this is an abstract class and cannot be used directly.** Part of the traffic prediction model realizes prediction by modeling the closeness/period/trend. By default, the data of `len_closeness`/`len_period`/`len_trend` is used to predict the data at the current moment(a single-step forecast). The [Batch](../data/batch.md) object generated by this class contains 4 keys: `X`, `y`, `X_ext`, `y_ext`. Here `len_closeness`/`len_period`/`len_trend` are parameters for data, see [here](../data/args_for_data.md) for details. 

- `TrafficStatePointDataset`

  A class inherited `TrafficStateDataset` for traffic state prediction. The dataset is used for point-based/segment-based/region-based dataset as long as the spatial dimension of this data set is 1-dimensional. The shape of tensor in the [Batch](../data/batch.md) object generated by this class is 3-dimensional, namely `space_dim, time_dim, feature_dim`.

- `TrafficStateGridDataset`

  A class inherited `TrafficStateDataset` for traffic state prediction. The dataset is used for grid-based dataset. The shape of tensor in the [Batch](../data/batch.md) object generated by this class is 3-dimensional or 4-dimensional depends on parameter `use_row_column`. If set `use_row_column=True`, then the 4 dimensions are `grid_row_dim, grid_column_dim, time_dim, feature_dim`. Otherwise, the 3 dimensions are `space_dim, time_dim, feature_dim`, in this case the grid is renumbered in one dimension.

- `TrafficStateOdDataset`

  A class inherited `TrafficStateDataset` for traffic state prediction. The dataset is used for od-based dataset, which means origin and destination. The shape of tensor in the [Batch](../data/batch.md) object generated by this class is 4-dimensional, namely `origin_dim, destination_dim, time_dim, feature_dim`.

- `TrafficStateGridOdDataset`

  A class inherited `TrafficStateDataset` for traffic state prediction. The dataset is used for grid-od-based dataset. The shape of tensor in the [Batch](../data/batch.md) object generated by this class is 4-dimensional or 6-dimensional depends on parameter `use_row_column`. If set `use_row_column=True`, then the 6 dimensions are `origin_grid_row_dim, origin_grid_column_dim, destination_grid_row_dim, destination_grid_column_dim, time_dim, feature_dim`. Otherwise, the 4 dimensions are `origin_dim,  destination_dim, time_dim, feature_dim`, in this case the grid is renumbered in one dimension.
  
- `MapMatchingDataset`

  Base class for all map matching tasks. This class generates a dictionary which contains 3 keys:`rd_nwk`, `trajectory` and `route`, representing road network, trajectory of GPS samples and ground truth respectively. if the dataset have `with_time=True` and `delta_time=True` is set, `trajectory` will include a `time` column indicating the reading of the seconds. `delta_time` is a parameters for dataset, see [here](../data/args_for_data.md) for details. see [here](../usage/standard_track.md) for introduction of standard data input.

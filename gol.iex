defmodule GameOfLife do

  def iterate(living_cells) do
    neighbor_pairs = Enum.flat_map(living_cells, &neighbor_cells_for/1 )
    |>  Enum.map(fn(c) -> {c, 1} end)
    live_pairs =  Enum.map(living_cells, fn(c) -> {c, 0.5} end)
    all_pairs = live_pairs ++ neighbor_pairs
    filtered_totals = Enum.map(all_pairs, &pair_to_point/1)
                 |> Enum.uniq
                 |> summed_reduced_points(all_pairs)
                 |> apply_game_rules

    Enum.map(filtered_totals, &pair_to_point/1)
  end

  def neighbor_cells_for(v) do
    [ point_diff(v, -1, -1),
      point_diff(v, -1,  0),
      point_diff(v, -1,  1),
      point_diff(v,  0, -1),
      point_diff(v,  0, +1),
      point_diff(v, +1, -1),
      point_diff(v, +1,  0),
      point_diff(v, +1, +1)
    ]
  end

  def point_diff(point, x_diff, y_diff) do
    {elem(point,0) + x_diff,elem(point,1) + y_diff}
  end

  def pair_to_point(p) do
    elem(p,0)
  end

  def summed_reduced_points(transformed_points, all_pairs) do
    Enum.map(transformed_points, fn(point) ->
      value = Enum.filter(all_pairs, fn(pair) -> elem(pair, 0) == point end)
              |> Enum.reduce(0, fn(p, accum) -> elem(p,1) + accum  end)
      {point, value}
    end)
  end

  def apply_game_rules(transformed_points) do
    Enum.filter(transformed_points, fn(pair) ->
      (elem(pair, 1) > 2) && (elem(pair, 1) <= 4)
    end)
  end

end
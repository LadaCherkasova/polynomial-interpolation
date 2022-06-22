import matplotlib.pyplot as plt
import numpy as np

def get_data(file_name):
     data = []
     file = open(file_name, "r")

     while True:
          line = file.readline()
          if not line: break
          time, coord_x, coord_y, vel_x, vel_y = [int(key) for key in line.strip().split(' ')]
          list = {'time': time, 'coord': [coord_x, coord_y], 'vel': [vel_x, vel_y]}
          data.append(list)

     file.close()
     return data

def mark_via_points(data):
     for i in range(len(data)):
          plot_trajectory.scatter(data[i]['coord'][0], data[i]['coord'][1], color="red")

def count_coef(index, delta_t, isX):
     coord_cur = data[index]['coord']
     vel_cur = data[index]['vel']
     coord_next = data[index + 1]['coord']
     vel_next = data[index + 1]['vel']
     i = 0 if isX else 1

     a0 = coord_cur[i]
     a1 = vel_cur[i]
     a2 = (3 * coord_next[i] - 3 * coord_cur[i] - 2 * vel_cur[i] * delta_t - vel_next[i] * delta_t)/(delta_t ** 2)
     a3 = (2 * coord_cur[i] + vel_cur[i] * delta_t + vel_next[i] * delta_t - 2 * coord_next[i])/(delta_t ** 3)

     return a0, a1, a2, a3

def plot_graphs(data):
     for j in range(len(data)-1):
          delta_t = data[j+1]['time'] - data[j]['time']
          t = np.linspace(0, delta_t)
          t_common = np.linspace(data[j]['time'], data[j + 1]['time'])
          a0_x, a1_x, a2_x, a3_x = count_coef(j, delta_t, True)
          a0_y, a1_y, a2_y, a3_y = count_coef(j, delta_t, False)

          x = a0_x + a1_x * t + a2_x * t ** 2 + a3_x * t ** 3
          y = a0_y + a1_y * t + a2_y * t ** 2 + a3_y * t ** 3
          dx = a1_x + 2 * a2_x * t + 3 * a3_x * t ** 2
          dy = a1_y + 2 * a2_y * t + 3 * a3_y * t ** 2

          plot_coordinates.plot(t_common, x, color='orange')
          plot_coordinates.plot(t_common, y, color='green')
          plot_velocity.plot(t_common, dx, color='orange')
          plot_velocity.plot(t_common, dy, color='green')
          plot_trajectory.plot(x, y)


fig = plt.figure()
plot_coordinates = fig.add_subplot(2, 2, 1)
plot_coordinates.set_title("coordinates"), plt.grid()
plot_velocity = fig.add_subplot(2, 2, 2)
plot_velocity.set_title("velocity"), plt.grid()
plot_trajectory = fig.add_subplot(2, 2, 3)
plot_trajectory.set_title("trajectory"), plt.grid()

data = get_data("test_data.txt")
mark_via_points(data)
plot_graphs(data)

plot_coordinates.legend(['coord_x', 'coord_y'])
plot_velocity.legend(['vel_x', 'vel_y'])
plt.show()

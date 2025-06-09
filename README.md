# AssetyDlaMnie
https://rvros.itch.io/animated-pixel-hero
nie moje
def rozjasnij_powierzchnie(surface, wartosc=50):
    surface_copy = surface.convert().copy()
    arr = pygame.surfarray.pixels3d(surface_copy).astype(np.int16)
    arr += wartosc
    arr = np.clip(arr, 0, 255)
    arr = arr.astype(np.uint8)
    pygame.surfarray.blit_array(surface_copy, arr)

    return surface_copy

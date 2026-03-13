NuLite con postprocessing di CellVit++ tramite CPU.

Ho usato come base NuLite (https://github.com/CosmoIknosLab/NuLite), e ho modificato alcune parti di codice in base al post-pricessing CPU di CellViT++ (https://github.com/TIO-IKIM/CellViT). Le modifiche apportate sono le seguenti:

1. Copiato il file "cellvit/models/cell_segmentation/postprocessing.py" in NuLite e cambiato l'import in nulite.py:
----------------------------------------------------------------
# PRIMA
from nuclei_detection.utils.post_proc_nulite import DetectionCellPostProcessor

# DOPO
from nuclei_detection.inference.postprocessing import DetectionCellPostProcessor
----------------------------------------------------------------

2. Aggiunto in postprocessing.py le funzioni importate mancanti nel progetto NuLite: get_bounding_box e remove_small_objects

3. Modificata la seguente parte di codice in nulite.py
----------------------------------------------------------------
# PRIMA
instance_pred = cell_post_processor.post_process_cell_segmentation(pred_map)
instance_preds.append(instance_pred[0])
type_preds.append(instance_pred[1])

# DOPO
instance_pred, type_pred = cell_post_processor.post_process_single_image(pred_map)
instance_preds.append(instance_pred)
type_preds.append(type_pred)
----------------------------------------------------------------
# Parsing and Reading Data

def __check_labels(img_path: str, lbl_path: str) -> bool:
    '''
    Check if pair of labels and images exist. Filter non-existing pairs.
    '''
    name = os.path.basename(img_path)
    name, ext = name.split('.')
    name = name.split('_')[:-2]
    name = '_'.join(name)
    names = []
    for l in ['color', 'instanceids', 'labelids']:
        # Check if label exists
        lbl_name = name + '_' + l + '.' + ext
        if not os.path.exists(os.path.join(lbl_path, lbl_name)):
            return False, None
        names.append(lbl_name)
    return True, names
def __goose_datadict_folder(img_path: str, lbl_path: str):
    '''
    Create a data Dictionary with image paths
    '''
    subfolders = glob.glob(os.path.join(img_path, '*/'), recursive = False)
    subfolders = [f.split('/')[-2] for f in subfolders]
    valid_imgs = []
    valid_lbls = []
    valid_insta= []
    valid_color= []

    datadict = []

    for s in tqdm.tqdm(subfolders):
        imgs_p = os.path.join(img_path, s)
        lbls_p = os.path.join(lbl_path, s)
        imgs = glob.glob(os.path.join(imgs_p, '*.png'))
        for i in imgs:
            valid, lbl_names = __check_labels(i, lbls_p)
            if not valid:
                continue

            valid_imgs.append(i)
            valid_color.append(os.path.join(lbls_p, lbl_names[0]))
            valid_insta.append(os.path.join(lbls_p, lbl_names[1]))
            valid_lbls.append(os.path.join(lbls_p,  lbl_names[2]))

    for i,m,p,c in zip(valid_imgs, valid_lbls, valid_insta, valid_color):
        datadict.append({
                'img_path': i,
                'semantic_path': m,
                'instance_path':p,
                'color_path': c,
            })   

    return datadict

def goose_create_dataDict(src_path: str, mapping_csv_name: str = 'goose_label_mapping.csv') -> Dict:
    '''
    Parameters:

        src_path            :   path to dataset

    Returns:

        datadict_train      : dict with the dataset train images information

        datadict_val        : dict with the dataset validation images information

        datadict_test       : dict with the dataset test images information
    '''
    if mapping_csv_name is not None:
        mapping_path = os.path.join(src_path, mapping_csv_name)
        mapping = []
        with open(mapping_path, newline='') as f:
            reader = csv.DictReader(f)
            for r in reader:
                mapping.append(r)
    else:
        mapping = None

    img_path = os.path.join(src_path, 'images')
    lbl_path = os.path.join(src_path, 'labels')

    datadicts = []
    for c in ['test', 'train', 'val']:
        print("### " + c.capitalize() + " Data ###")
        datadicts.append(
            __goose_datadict_folder(
                os.path.join(img_path, c),
                os.path.join(lbl_path, c)
                )
            )

    test,train,val = datadicts

    return test,train,val, mapping
